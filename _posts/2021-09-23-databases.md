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
Why do we need databases?

**Trunk:**\
General overview of different types of databases, and a list of widely-used databases of that type.

**Branch:**\
Concerte deep-dive into each type of database, with examples.

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

## Trunk

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

#### Document Store
This is typically what I think of when I think NoSql. You can almost think of each *entry* in the database as a *json* that has nested fields. Then the *query* is also a *json* specifying the key-value pairs that the results should be filtered on. It’s perfect for things like storing a blog post, comments, tags, etc, all in one document. 

What it’s not good for is for complex queries or queries needing joins across multiple tables. You kind of want your document to contain *all* the information you need. Otherwise you’ll have to make another query to get the additional information since you *can’t join* with other tables.  

Things like blogging platforms could be a perfect use-case for this - you can use a single query to pull up a document that contains the blog post, comments, tags, etc. No other complex operations. You can fetch the entire blog page in a simple query. Companies like Facebook and Amazon have perfect use-cases for this. Facebook could store all the contents of your wall in one document: urls to your featured photos, posts and likes, etc. And it can just store your most recent 10 posts that you see when the page loads, then when you scroll, it can make another query to fetch more post. Those additional posts could be stored in the same database as a different document, or it could be stored somewhere else that has cheaper storage but takes longer to query. Because how many times will you be scrolling through old posts anyway. These are the types of considerations you might have while building out a product and deciding which databases to use for which data. 

	mongoldb, couchdb, elasticsearch

#### Column-Oriented Stores
This is probably the most similar to your relational SQL database. On the surface it looks like SQL to the user, but under the hood the data is stored differently. You guessed it, it’s stored by columns rather than by rows. This is mostly used for analytics purposes where you’re aggregating a small number of columns over a lot of rows. todo: sql or nosql?

	Cassandra, Hadoop Hbase, Redshift, Clickhouse, Snowflake

#### Graph Databases
This, to me at least, is one of the more obscure not-yet-widely-used nosql databases. Apparently it can be used for social networks, fraud detection, search, etc. It’s built to depict relationships (edges) between datapoint (nodes). Like how your Facebook friends are connected and what they’ve liked, what pages or events they’re on, and so on and so forth. Neo4j is apparently the most popular, and apparently companies like Lyft, Airbnb and Ebay use it. 

	Neo4j, ArangoDB and OrientDB

#### Object Databases
This is also right up there with Graph Database where it’s not all that popular. I personally have never used it. I assume it is what is sounds like.
Todo

	Wakanda, Object Store. 

## Branches

### Key Value Store

Key Value store can be further split into in-memory vs on-disk (classic) databases. 

#### In-Memory
**Redis** and **Memcached** are the two most popular in-memory key-value databases. Both are in-memory databases (in contrast to the other databases mentioned here which are stored on disk) which are most popular for being used as *caches*. For example, if you’re trying to load your amazon shopping cart, during the first load, that request may be served from the database, looking up your cart_id, and getting the response of items in the cart. That key (cart_id) and value (list of items) will be stored in memory in essentially a hashtable. The next time you load your cart it can be served from the in-memory key-value cache. It’s easy to use, essentially like a HashTable, and supports a lot of different dataypes. Of course, the devil is in the details here with invalidating or modifying the cache when the entries change, but I believe <todo> this is largely handled by the software. Some things to consider when evaluating which to use are: whether it can perist data to disk, what datastructures and languages are supported, what features it has, whether it’s thread-safe, support for sharding and distribution and so on. Both Redis and Memcached are open-source.

**Who uses Redis?** Snapchat, Github, Twitter, Pinterest, Stack Overflow
**Who uses Memcached?** Facebook, Apple

#### On-Disk

The Key Value Stores that are stored in disk are also often referred to as **wide-column**. I’ve seen it be used for analytics use-cases. It stores data for specific use cases. You can think of it as being a Map<Map<Obj, Value>>. For example, if I know I’m going to be querying shows has been watched in a certain streaming service in a certain country on a particular date, then I might store my data in BigTable, a wide-column key-value store, like this:
	
```Date —> {Show, StreamingService, Country} —> Value```

You can see that this will be very quick, because it has the great performance from the `Key—> Value` structure but it’s also very inflexible in that, literally any other type of query might require you to jump through hoops to do or not even be possible at all. For example, unless you specifically store a ‘Global’ key (or your database is optimized such that if you omit the country, it will know how to handle it - I don’t know of any that do that), you’d have to keep a list of the countries and query all of them and sum in your service. The Date is often referred to as the row and the {Show StreamingService, Country} as the Column Family. You might be wondering how this is really different from relational or anything and it seems like it’s just being explained differently. The difference, partially, comes down to the way it’s stored on disk - the columns for each row are stored together. So all the information for a certain date will be lumped together, and even from there, it’s super fast performance to get results for a combination of query parameters. It’s also very flexible in the sense that the columns can be anything - and there can be billions of columns (hence wide-column), and it can be very sparse. 
Now, there’s also key-value stores that operate primarily from storage, like **Amazon’s DynamoDB**. Then what makes this different from a relational database that has an index on certain columns, you ask? Well, the value can be anything! That’s where the flexibility of nosql comes in, the schema of the value can be whatever you want it to be. In our shopping cart example, it could be a list of items, it could be an empty cart with just the cc details, it could be just the shipping address. In addition, because it’s noSQL it comes with all the scalability bonuses, and can be partitioned and scaled. And because it’s managed <todo> all that will be taken care of for you under the hood. 
Who uses DynamoDb?  Netflix, Lyft, Tinder, Airbnb, Snap, Amazon
DynamoDb is Amazon’s key-value database, Google has it’s own called LevelDB but it’s not nearly as popular or widely used. 
	
#### File-System
Then there’s the file systems. Amazon has a file system storage in the cloud called **S3** and Google has a file system storage in the cloud called **GCS: Google Cloud Storage**. It is essentially just like the file system on your computer but is stored in Amazon/Google’s servers. It can be considered a key-value store because the key will be the filename and the value will be the contents of the file. The most common use cases I’ve seen for this are to store images, and then to store the url for those images in some other database, where yoou can retrieve the url if you have the image_id, for example. One drawback is that accessing this could be a bit on the slower side. An generally these files will be read-only. On the other hand, this type of storage is very cheap. So it’s often used to store data that’s rarely ever accessed but need to be kept around just-in-case. I’ve read that amazon stores really old purchase history in s3 files. They can be read-only because the order can no longer be changed. And they can be kind of slow because it may be rare for someone to be accessing data that is 2 years old.
The other use case for file systems is in analytics use cases, which we will explore in more detail in another blog post. 

**Customers:** Spotify, WePay, Plaid
	
## Document

### MongoDB
	
You might’ve heard of **MongoDB**. It was only founded in 2007 but it’s become very popular very quickly. It’s your classic document-based database. You give it some key-value fields in a json to filter down your results, and you have your results. It also has all the perks of nosql like high availability and sharding for horizontal scaling.
	
At it’s most basic, an inserting an entry into a mongoDB table for blogs posts could look like:

```
db.post.insert( {
	Title: “Know Your Databases”
	Description: “A conversational introduction to databases”
	Content: “Databases are huge. You gotta know them….”
	Comments: [
		{ user: “user1”,
		  message: “great content!”
		  }
	]
```
	
And it would basically just stick it into the database.
	
And the most simple query to retrieve this document:

```db.post.find({“Title”: “Know Your Databases”})```
	
You may be thinking, it seems restrictive to not be able to do joins. How many use cases could there be for something like this that also needs to take advantage of the ability to scale a lot? Well Facebook could be an example - I could imagine all the contents of your wall being in a document. And multiply that by 2 billion users.
	
Here’s a personal tidbit about my experience with a Document based database: **ElasticSearch**. The use case here was that we were building a Search tool for many business’ websites, and we used ElasticSearch to store an entry every time a user searched for something. We’d store the search query, the results that came up, what the user viewed and clicked on, etc. Then we’d use this data to show the business analytics behind this, and recreate the search results that the user saw. Food for thought.
	
**Customers:** Forbes, Toyota, KPMG, Verizon, Cisco, Google 

## Column-Oriented Stores
	
This type of database is a specialized version of SQL. It’s optimized to query a small set of columns but across a large amount of rows. For example, if I want to query for the number of times 'The Office' was watched every day for the past five years in a table that had an entry for each date and the columns were the number of watches, unique viewers, favorited, etc. A column oriented store has great performance for this because the way this type of database stores data is it stores the columns together on disk. So we could read one chunk from the disk and have all our data, whereas in a regular SQL database it might have to read data that’s stored spread across the disk. 
You might even hear this type of database be referred to as a Warehouse, we’ll have a separate blog post for just analytical databases (todo). One major thing to watch for in this databases, from my experience, is whether it’s a *managed* database or not. What does that mean? Whether things like scaling, sharding, partitioning, optimizations and maintenance are taken care of under the hood, or if you’ll spend a lot of time manually tuning your database, getting extra machines when the data grows, etc. For example, I’ve used Redshift from Amazon which is managed, where I basically just had to worry about writing and reading data, and I’ve used Clickhouse where we had to pay close attention to sharding and scaling.
A little disclaimer here that column-oriented databases are actually somewhere in between nosql and sql, IMO. They use PostgreSQL, which is a dialect of SQL but it may not enforce all of the constraints needed to make it relational. (Todo)

Notice again that column-oriented datastore are totally different from the wide-column stores we talked about above. 
	
## Graph Database

First, lets talk about the difference between **GraphQL** and **graph databases**. GraphQL itself is not a database like MySQL. It’s a server with an API that takes in a request in a specific form (kind of like json). You can think of the format that it takes in as it’s query language, kind of like how SQL is a query language. While SQL will look like SELECT <columns> FROM <table>, GraphQL’s request will look like {query { User(id: “er3tg429”) {name posts {title} followers (last:3) {name}}}}. So how does GraphQL work as an API? So what is the database that you can use with this query language? Well, it can be any database. How can it be any database? Again, going back to the fact that GraphQL is actually an API server, what it does is It expects a json-like request and will translate it to query whatever database you’re using for the response. So what does this look like concretely? If it’s a SQL database, then in the graphQL server you’re using, you’ll add a configuration that says that if the request to the server looks like this: {“”””} then translate it to: `select * from customers where name=“” and location=ny;`

So what’s the story behind GraphQL? How did it come about, how does it get used and what’s the benefit of using GraphQL? Well it got created by Facebook, and that in itself says a lot about why it was created. Facebook contains a mountain of data, a mountain the size of Mount Everest. It’s likely stored in all kinds of databases and there’s tens of thousands of engineers at Facebook collecting all this data and running all sorts of Machine Learning algorithms to determine what ad to show you next to make some $$ or what instigating article to show on your newsfeed to get a reaction or have you share it. Anyway, back to GraphQL: one benefit is that it lets you use any underlying database using the same syntax for the query requests. Then once a team has created this GraphQL server for their database, then all the teams that use that server can be agnostic to the underlying database. I think of it as almost a wrapper around databases, that enforces what the request should look like. 

> **Declarative vs Imperative Programming**
>> This is also a good place to talk about declarative vs imperative programming. A lot of the software you’ve likely been working with so far has likely been imperitive - meaning, it’s procedural. When you write a method, you’re telling the computer what to do and how to do it - like, loop through a list and print out each item. Declarative is when you just tell the computer what you want and let the computer figure out how to get you that. SQL and GraphQL are both declarative - you tell the computer you want these fields that match this requirement, and the computer (in this case the database) figures out how to go through all the data and get you what you’re looking for. For instance, you’re not writing code that tells the database specifically to do a linear or binary search through all the data and return the data that matches. But what you DO do is, when you first create that database, you’ll specify indices that help your database do it’s job better. Like you’ll say that the customer_id is your index, telling the database - hey I’m going to be asking you to look for a specific customer id, so you better store all this data in a way that you can find a specific customer_id that I ask for pretty quickly.

>> A lot of your regular backend programming will be imperetive. Database languages are declarative. Configurations for your servers are declarative. Functional programming languages are declarative. 

Neo4j seems to be the popular database that has “native” graph storage. I guess that means that the database itself was built to be optimal for querying with the graphQL syntax. 

If you’re interested in any of these in particular, it can’t hurt to build your own leaves (and honestly fill out the rest of this branch) on your own!

**Customers of Neo4j:** Lyft, airbnb, adobe, caterpillar, volvo 
