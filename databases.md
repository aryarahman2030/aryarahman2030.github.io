layout: page
title: "Know Your Databases"
permalink: /databases/

Databases are huge. You’ve gotta know them. 
They’re going to come up all the time, in your work and in your interviews. 
If you learn them up front, you save yourself a lot of head scratching and confusion in the long run. 

Throughout the span of your career, you’ll come across all kinds of names like `Elasticsearch` and 	`Redshift`. 
If you *Know Your Databases* you’ll be able to categorize them from the get-go, instead of being in the dark and trying to find your way around. 
As an added bonus, you’ll also need to know a lot about databases to ace your systems design interviews, and based on how you come across here has a big impact on what leveling you get placed in at the company, and how experienced you come off. 

*Roots:*\
What are the different types of databases and why do we need them?

*Trunk:*\
Different types of databases, and what each one is good for

*Branch:*\
More details and what are industry-standard frequently used database systems?

*Leaves:*\
Build Your Own Leaves

## Roots

Databases are used to store and access data. What type of data, you ask? 
Everything from your Facebook photos and posts to YouTube videos to your financial data, to amazon inventory and orders. 
Your tweets to your healthcare records, to your email, your pay statements and taxes and more. The list is endless. 

Then there’s analytics and historical data that a lot of companies hold, that track everything from what videos you watched to what tweets you looked at and for how long, to what songs you listened to, to what car rides you took. This type of data, we'll get into in the next blog post.

Almost everything that you look at on an electronic device, unless it’s saved to your device, ultimately comes from some database, somewhere. 
As you probably noticed, there are many different types of data (photos, videos, text, etc), and different use cases for the data (access your own, look up a specific item, look up analytics for the past five years). We’ll go into how different types of databases are better suited for different cases.

That’s the breadth of the types of data and then there’s the aspect of depth. When I say depth, I mean the scale of data that we now generate and store. We generate *2.5 quintillion* bytes of data every day. That’s 1000^18 bytes everyday. And the rate at which we generate data is accelerating. Just in the last two years we generated 90% of the total data. And as we connect more and more devices to the internet (refrigerators, cars, lightbulbs even) and as we move on to 5G to make the speed of data transfer even faster, the amount of data generated is just going to explode. 

What are we doing with so much data,  you ask? If you do a google search to find an article from 10 years ago, that’s going to be need to be stored in a database that can be accessed and returned to you. 
Data is also the new oil in the sense that, your personal data and data about your behavior and actions on the internet are invaluable to companies that can then use all this data to monetize you and show you the best ads. Or in the case of self-driving cars, analyze driving patterns and use machine learning to continue to learn to drive better. The challenges can be like finding a needle in a haystack (e.g. google search), or like dumping out the whole haystack (using your behavioral history to show you ads). 
We need efficient databases and efficient design of datastore to make accessing different types of data in all these different ways performant.