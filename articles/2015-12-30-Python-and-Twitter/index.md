# Python and the Twitter API

Run basic text analytics on a collection of Tweets

The Twitter API allows us to collect data based on a particular keyword, user handle, or hashtag.  We can filter those results by language, geographic location, and either the latest, most popular tweets, or tweets within a specified timeframe. Also, the API provides some tools to run basic text analytics such as finding entities in a particular collection of tweets. To collect and run basic text analytics in a collection of tweets:

* Connect to the API
* Search Tweets
* Extract Tweet entities

## Connect to the Twitter API:
To establish a successful connection with the API we first need consumer and oAuth tokens from a newly created [Twitter App](https://apps.twitter.com/), like so:

```
import twitter

def oauth_login():
    CONSUMER_KEY = '0pJAid2aqrRtgwe6dKvPAerp8b'
    CONSUMER_SECRET = 'rfrb0fbGgCvpf1sgtRd7OsrBCT7p8DPWuB8WpeLJ9LfelJW8sp'
    OAUTH_TOKEN = '15648766-lxT6QBxMgp69gFDsef6FI4KqporqqvOyd4U5t4qD7'
    OAUTH_TOKEN_SECRET = 'KYdm5roVu2xMlo5asSDfs1LGHwYBRL0Gxi5IkXMRZLsuJR2'

    auth = twitter.oauth.OAuth(OAUTH_TOKEN, OAUTH_TOKEN_SECRET, CONSUMER_KEY, CONSUMER_SECRET)

    twitter_api = twitter.Twitter(auth=auth)
    return twitter_api
```
Make sure you substitue the tokens with your own credentials as the above keys are just place holders and will not work.

## Search Tweets
Lets define two functions. One to find Tweets based in our criteria, and then, another function to select the most favorited Tweets from that collection:

```
# Language = English
# Result type =  recent or popular
# count = how many tweets to return
# geocode = “latitude,longitude,radius”, for example, “"37.781157,-122.398720,10mi"”
#           will limit the results for tweets within 10 miles of San Francisco
# Other parameters not used but available: until, since_id, max_id

def twitter_search(twitter_api, q, max_results=200, **kw):  
    search_results = twitter_api.search.tweets(q=q, count=100, lang='en', result_type='recent',  geocode= "37.781157,-122.398720,10mi", **kw)  
    statuses = search_results['statuses']
    
    max_results = min(100, max_results)
    
    for _ in range(10):
        try:
            next_results = search_results['search_metadata']['next_results']
        except KeyError as e:
            break

        kwargs = dict([ kv.split('=') 
                        for kv in next_results[1:].split("&") ])

        search_results = twitter_api.search.tweets(**kwargs)
        statuses += search_results['statuses']
        
        if len(statuses) > max_results: 
            break
            
    return statuses

def find_popular_tweets(twitter_api, statuses, retweet_threshold=30):
        
    return [ status
                for status in statuses 
                    if status['retweet_count'] > retweet_threshold ] 
                    
twitter_api = oauth_login()
q = "surf"

search_results = twitter_search(twitter_api, q, max_results=20)
popular_tweets = find_popular_tweets(twitter_api, search_results)

print ("************POPULAR TWEETS*********************")
print ("************(TWEET, RE_TWEET COUNT*************")
print ("")
for tweet in popular_tweets:
    print (tweet['text'].encode('utf8'), tweet['retweet_count'])

```

## Extract Tweet entities
Create a function that extracts Tweet entities such as user handles, hashtags, and URLs from our collection.

```
def extract_tweet_entities(statuses):
    if len(statuses) == 0:
        return [], [], [], []
    
    screen_names = [ user_mention['screen_name'] 
                         for status in statuses
                            for user_mention in status['entities']['user_mentions'] ]
    
    hashtags = [ hashtag['text'] 
                     for status in statuses 
                        for hashtag in status['entities']['hashtags'] ]

    urls = [ url['expanded_url'] 
                     for status in statuses 
                        for url in status['entities']['urls'] ]

    return screen_names, hashtags, urls

# provides the entity and the frequency for each collection
def get_common_tweet_entities(statuses, entity_threshold=3):
    tweet_entities = [  e
                        for status in statuses
                            for entity_type in extract_tweet_entities([status]) 
                                for e in entity_type 
                     ]
    c = Counter(tweet_entities).most_common()

    return [ (k,v) 
             for (k,v) in c
                 if v >= entity_threshold
           ]

twitter_api = oauth_login()
q = "surf"

search_results = twitter_search(twitter_api, q, max_results=20)
popular_tweets = find_popular_tweets(twitter_api, search_results)

statuses = twitter_search(twitter_api, q)
screen_names, hashtags, urls = extract_tweet_entities(statuses)


print ("************Tweet Entities*********************")
print ("***********************************************")
print ("")
print ("**************TOP 50 HANDLES*******************")
# json.dumps([dict(mpn=pn) for pn in lst])
print (json.dumps(screen_names[0:50], indent=1))
print ("")
print ("**************TOP 50 HASHTAGS*****************")
print(json.dumps(hashtags[0:50], indent=1))
print ("")
print ("**************TOP 50 URLs*********************")
print(json.dumps(urls[0:50], indent=1))
print ("")

common_entities = get_common_tweet_entities(search_results)

print ("*****************************************************")
print ("************Most Common Entities*********************")
print (common_entities)
print ("*****************************************************")
print ("*****************************************************")


# calculate average number of words per tweet:
def analyze_tweet_content(statuses):
    if len(statuses) == 0:
        print ("No statuses to analyze")
        return
    
    def average_words(statuses):
        total_words = sum([ len(s.split()) for s in statuses ]) 
        return 1.0*total_words/len(statuses)

    status_texts = [ status['text'] for status in statuses ]
    screen_names, hashtags, urls, _ = extract_tweet_entities(statuses)
    
    words = [ w 
          for t in status_texts 
              for w in t.split() ]
    
    print ("Averge words per tweet:", average_words(status_texts))
```

To find the account that owns the most favorited tweets of a person:
```
# Analyze a user's favorite tweets. Insert user handle
analyze_tweet_content(search_results)
print ("*****************************************************")
print ("*****************************************************")
analyze_favorites(twitter_api, "theebecky")
```

The full code can be found [here]()