# What database should I use?
Use a relational database like PostgreSQL unless you have a specific reason not to

### When to use MongoDB?
Never.

MongoDB is a document-oriented database. These type of databases do not have the concept of tables or predefined columns; instead, document databases store data as a collection of records without schemas, structure or relations to other records. In MongoDB's case, it stores the data under collections (instead of tables) where each row of the collection is one JSON object (without columns).

You'll find many articles talking you out of using MongoDB, so let's skip that part. Something important to note is that many of those articles are written by users that dislike MongoDB for the wrong reasons: they've tried to use a document database when dealing with relational data. And even though it is somewhat forgivable because schema design is hard, using document storage when dealing with relational data is a poor architectural choice (at least most of the time).

There are other articles telling you that you shouldn't use MongoDB because it is a poorly engineered storage option run on marketing and not on technical merit. There are security and support issues have been part of MongoDB since its inception making it a poor choice even if you do need a document store. Those are the better reasons to stay away from MongoDB.

Because most data is relational, use cases of databases that are designed to store, represent, or work with documents tend to be very specific. A search engine that is constantly executing queries that require more than matching an exact string is one example:

![](https://i.imgur.com/QOcPX3r.png)

Notice how the results of querying "longboarding in bolinas" yields results that don't exactly match the input string. If we had to join data from different tables (or even from the same table) in order to get those results, it could take a long time; instead, we can do a faster search by querying a document database that stores a 'denormalized' version of the data which could then be used to create normalized search indexes.

An example of the indexing process is when variants of a term are mapped to a single, standardized form. For instance mapping _"surfing"_ and _"surfer"_ to _"surf"_ ignoring the distinction between _surfing_ and _surfer_. This is why when using normalized search indexes, a query for _"longboarding in bolinas"_ (["longboard", "bolinas"]) could yield its exact match  _"longboarding in bolinas"_ and also other results including similar phrases such as _"Continue on to Bolinas, which has stellar longboard waves..."_.

Full-text search engine queries could get very complex. The main record and all of its related searchable data should be in a single object -- even if some of that related data would *normally* be part of a separate record. This means faster results because with one lookup you are able to get the applicable record instead of following relations.

### Which are the best document stores?
It depends on your requirements. Cases where document storage is the right solution are almost always really specific, like the previous search example. It also just so happens that PostgreSQL can be used as a document store, because you can store and work with arbitrarily nested data (through a JSONB column and the associated json_* functions). It's not something commonly used but it can be useful in some cases like for API scraping (so that you can store the original API response even if its exact format may vary over time, outside of your control or knowledge).

A better question would be something like "If I want to build a search engine, what are the best solutions?" in which case you might consider ElasticSearch (or the underlying tech, Lucene).  The usual answer to "What database should I use?" is **"Use an RDBMS like PostgreSQL unless you have a specific reason not to"**.
