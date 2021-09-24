---
layout: post
---

Databases are huge. You’ve gotta know them. 
They’re going to come up all the time, in your work and in your interviews. 
If you learn them up front, you save yourself a lot of head scratching and confusion in the long run. 

Throughout the span of your career, you’ll come across all kinds of names like `Elasticsearch` and 	`Redshift`. 
If you *Know Your Databases* you’ll be able to categorize them from the get-go, instead of being in the dark and trying to find your way around. 
As an added bonus, you’ll also need to know a lot about databases to ace your systems design interviews, and based on how you come across here has a big impact on what leveling you get placed in at the company, and how experienced you come off. 

**Roots:**\
What are the different types of databases and why do we need them?

**Trunk:**\
General overview of different types of databases, and a list of widely-used databases of that type.

**Branch:**\
More details on each type of database

**Leaves:**\
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

## Trunk:

At the highest level, there’s just two types - **Sql** and **NoSql**. So let’s get to it!

### SQL
I’m assuming you already have some familiarity with SQL databases. In a majority of cases and companies, this is what is used. A majority of companies can get by using primarily sql databases. Large companies with products that most of the world uses (facebook, amazon, google) have had to turn to nosql because of the need to scale and remain performant.  

This will probably be the first type of database that you use, and is the one that you’ll come across most frequently. It’s your standard relational database. It’s tried and tested. It’s best for when you access data based on a few fields, like a user_id, that you can index and make lookup fast. And it’s best for storing text - strings or numerical values. And it’s best for when you need to join with other tables on certain fields. If you need to store an image or video, your best bet would be to store it elsewhere and store the url to access that in the database.

That's basically it for SQL, so we'll go off on some tangents before moving onto NoSQL:

>**Twig - Database, Cluster, RDBMS**
>>SQL databases are called relational databases because data ‘related’ to each other can be stored across multiple tables in the database and accessed together with ‘joins’ which has great performance in SQL databases (but not in NoSQL.. we’ll get into that later). Taking that one step further it’s often referred to as RDBMS which stands for Relational Database Management System. 
>>What’s the diffrence between databases and DBMS? They’re very closely related. DBMS is the actual system/software that you install on a computer that manages storing the data and retreiving it from the computer when it’s queried. A database is a set of tables. Technically it’s a “collection of data” This set of tables can be queried together through a ‘join’, for example. You can’t ‘join’ data from tables that are in different databases. For example, at a company you can have one database for product A and another database for product B, but they can both be in the same DBMS. In everyday work situations, I’ve also heard of ‘database’ being used when actually referring to DBMS. I may unintentionally do that in this post even. 
>>Then there’s ‘cluster’ which falls in the hierarchy between the two. The data in one database can be stored in a few different machines (we’ll get into it with ‘sharding’ below). All of these parts together will be a ‘cluster’. Below is a helpful visualization.

>**Twig - SQL vs MySQL**
>>Some more terminology and clarifying points - SQL is the language, and there are many databases that use “dialects” of SQL to query a database. The most popular types of SQL DBMS are Oracle, MySQL, Microsoft SQL Server, PosttgreSQL. Each one uses SQL and has some advanced functionality built on top of SQL, but has to be SQL compliant. (todo) I’ll stop here for SQL, unless you’re at a startup that is just setting up their SQL database, you won’t find the details of SQL databases all that relevant.

>**Twig - Scaling**
>>Where relational databases run into trouble is in scaling. Relational databases are vertically scalable, but they are not horizontally scalable. What this means is that you can scale it by adding more capacity like more disk space, compute and memory, but you can’t add more machines and split up the data across those machines. That’s horizontal scaling. 
>>Why does it matter how you scale? There’s tradeoffs between the two. Vertical scaling can be limited by what the largest machine you could possibly get is. Or what the maximum memory that you can get in one machine. That can get really expensive. So once you’ve used the largest machine with the most memory, you’ve hit a dead-end in terms of scaling even more. Horizontal scaling gets you a lot more flexibility with how much you can scale. You will have a set of machines each containing a portion of the data called “shard”. And it’s comparatively cheaper- you can get a whole bunch of cheap machines and split your data across them.  The overhead here comes from having another tool to coordinate this split-up data, and know where to direct incoming queries (todo we'll have another post about this). 
>>But relational databases don’t lend themselves to horizontal scaling because there’s no clear way to split up the data under-the-hood, and we would want to store them in one machine to be performant for the types of queries that relational databases get - one that uses joins. SQL queries give you a lot of flexibility in what kind of queries you execute to the point where you don’t know which data will be fetched from which table and combined in which way until you get the query.  So you can’t optimize on how you store the data across multiple machines to make sure you’re not having to query all the machines in a sub-optimal way. But if you store it in a single machine, you can still tune how to store the data to optimize how fast the lookup is (like indexing user_id example mentioned above).

So tl’dr - you can use relational tables in a lot of cases, will get great performance, it’s very commonly used and one of the oldest types of databases. With the exception that you expect your data to grow fast and you’ll have so much data that it’ll be hard to keep in a single machine.

Now to the interesting nosql databases!

### NoSQL
Naturally, now that we’ve talked about SQL, the next topic to broach is NoSQL. NoSQL gives you a lot of flexibility, both in terms of scaling and in terms of the data structure. Those are it’s two biggest selling points. NoSQL databases (some of them atleast..) don’t  have a specific table schema. For example, in some types of nosql databases, you can start off storing data that’s user_id and first_name. Then halfway through you can decide to start storing last_name too, and so on. How does this work? Because you have to be more careful when you’re querying that data. The difference between SQL and NoSQL is often referred to as “schema on write” vs “schema on read”. Because of this, when the type of your data changes in some way, you can continue using the same thing and just modify how you’re reading it to accommodate the new format. Whereas in SQL something like this may require a big migration process. 
NoSQL can be scaled horizontally. This means you can use cheap machines and can have your data size grow exponentially. 
NoSQL is a broad umbrella and there’s many different types of databases within this umbrella. We’ll take a look at each:

#### Key-Value Store
Let’s start with key-value. This is pretty simple! Almost like storing a hash table. It uses a hash table to store unique keys and points to a column which doesn’t need to have a specific type. It has great behavior since it’s essentially a constant time lookup, and scales easily. It can be used anywhere, where you need to do a simple lookup with a key, for example storing shopping cart data, or user preferences. It can also be used like a long-term, non-volatile cache. 

	redid, memcache, riak, BigTable, DyamoDB, Cassandra

#### 	Document Store
This is typically what I think of when I think NoSql. You can almost think of each entry in the database as a json, that has nested fields. Then the query is also a json specifying that the results should be filtered based on which keys match the values. It’s perfect for things like storing a blog post, comments, tags, etc, all in one document. What it’s not good for is for complex queries or queries needing joins across multiple tables. You kind of want your document to contain all the information you need. Otherwise you’ll have to make another query to get the additional information since you can’t make joins.  Things like blogging platforms will require a simple query to access it and not really any complex operations. You can fetch the entire blog page in a simple query. Companies like Facebook and Amazon have perfect use-cases for this. 
You might’ve heard of MongoDB. It was only founded in 2007 but it’s become very popular very quickly. It’s your classic document-based database. You give it some key fields in a json to filter down your results, and you have yoru results. It also has all the perks of nosql like high availability and sharding for horizontal scaling.

Who uses MongoDB? Google, Cisco, Facebook, Uber, Lyft, Intuit

If Amazon beat out google for key-value database, then Google beats Amazon for Document database. Google’s Firesbase is a lot more popular than DocumentDb.
Who uses Firestore? New York Times, The Economist, Instacart, Twitch. todo firestore vs firebase

	mongoldb, couchdb, elasticsearch

#### 	Column-Oriented Stores
This is probably the most similar to your relational SQL database. On the surface it looks like SQL to the user, but under the hood the data is stored differently. You guessed it, it’s stored by columns rather than by rows. This is mostly used for analytics purposes where you’re aggregating a small number of columns over a lot of rows. todo: sql or nosql?

	Cassandra, Hadoop Hbase, Redshift, Clickhouse, Snowflake

#### 	Graph Databases
This, to me at least, is one of the more obscure not-yet-widely-used nosql databases. Apparently it can be used for social networks, fraud detection, search, etc. It’s built to depict relationships (edges) between datapoint (nodes). Like how your Facebook friends are connected and what they’ve liked, what pages or events they’re on, and so on and so forth. Neo4j is apparently the most popular, and apparently companies like Lyft, Airbnb and Ebay use it. 

	Neo4j, ArangoDB and OrientDB

#### 	Object Databases
This is also right up there with Graph Database where it’s not all that popular. I personally have never used it. I assume it is what is sounds like.
Todo

	Wakanda, Object Store. 


