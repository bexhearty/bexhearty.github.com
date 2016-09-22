# Never forget to take your vitamins again
SmartThings, IFTTT, Zapier, and Slack to the rescue

When I worked at Segment, we built bots to complete annoying and mundane tasks. Wishing for something similar at home, I built a series of triggers so that Slackbot records the last time I took my vitamins and then reminds me when I need to take them again.

To begin, I used a [multipurpose sensor](https://shop.smartthings.com/#!/products/samsung-smartthings-multipurpose-sensor) from SmartThings (used to alert when a door or window opens or closes) and using [this](https://smile.amazon.com/Duck-282116-Printed-Inches-Single/dp/B00CJGF6EI/ref=sr_1_1?ie=UTF8&qid=1474492591&sr=8-1&keywords=duck+tape+owl)  awesome duck date, I taped it to the vitamin bottle:

![](https://cldup.com/BSgh11Oowo.png)

Next, for each time the sensor closes, I used an IFTTT recipe to trigger a Slack message telling me that I just took a vitamin:

![](https://cldup.com/MYzYmI2Fg2.png)

I also had to set another trigger to a Google sheet that records the time the bottle closed (since I wasn’t able to get IFTTT to properly send a `/remind` message to Slack):

![](https://cldup.com/1BVZAatq_m.png)

Lastly, I connected Zapier to that Google sheet and created a Zap to Slack with a `/remind me to take my vitamins in 12 hours` message:

![](https://cldup.com/UW2pYYnmzn.png)

If I get the slack message when I’m not near my vitamins, I can just hit `remind me in 15 minutes` option, and get a new notification later.  

![](https://cldup.com/siwQI7CEIT.png)

This reminder has been so helpful that I am going to replicate a similar project using a Raspberry Pi and a sensor connected to the dog food container. That way both my husband and I know when the dawgs have been fed and unfortunately for them, prevent double dinners.

