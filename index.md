
A lot of content out there about computer science, and software engineering is dry. And it’s scattered. And it’s filled with jargon. This blog is to cut all that out, and make software engineering accessible! This aims to come across like a friend who’s talking to you about software engineering colloquially, in plain English. 

How many times have you come across what’s supposed to be introductory explanations but that are like 

```Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.```

You basically have to already know what Kubernetes is to read about what Kubernetes is… 

The people who will get the most out of this blog software engineers in mid-career who have bits and pieces of knowledge but want to tie it all together and motivated new grads who have started their jobs in software engineering. It’s someone who has some background already and is looking to get a more solid foundation and fill gaps in their knowledge.

Hopefully it’s a starting point to give you a breadth of knowledge and pique your interest so you can go out there into the scattered world of information, sift through some of the jargon and go deeper in areas where you’re interested.

### What’s missing out there?
A lot of explanations start with a generic spiel like `XYZ is highly scalable, highly available and fault-tolerant`. To me, that’s like - ok that’s great if I’m already an expert and I’m evaluating your technology to actually adopt, but if I’m trying to learn, I don’t need for that to be the first sentence in the ‘Introduction’ or ‘Getting Started’ page. I don’t need to know right off the bat who the author of the paper that created it was. I don’t need to know what language it’s written in. What I want first is the elevator pitch, but it’s ridiculously hard, if not impossible to find that. 

What I really haven’t been able to find, is a simple TL’DR of many things related to computer science and software engineering. I often go on google, just wanting a simple explanation for something, and I find myself having opened 10 tabs, and reading through, essentially, sales pitches from companies that want you to adopt the technology, and giving up 30 minutes later after reading random pieces of information that I won't truly understand or remember because I have nothing to connect to. Try learning about zookeeper from the internet. I tried. After sifting through some content that either got into the weeds too quickly, or slow content that required me to sit through irrelevant information, or a high level broad-strokes using jargon but not really explaining intuitively what it is, I came out of that 30 mins feeling a little scattered, still only barely knowing at a high level what it does. 

```Zookeeper is a coordination service for distributed applications.```

Ok? 

```Kubernetes is a container orchestration technology.``` 

Ok? 

I’d much rather read or listen to a conversational exerpt about these things. Like reading a good NYTimes article, watching a good Vox clip, or listening to a good The Daily podcast. Unfortunately, we don’t really have anything like this for software engineering and tech. Well you have Wired and TechCrunch for tech, but nothing for understanding content about hardcore software engineering topics. In another sense, this blog is almost like a SparkNotes for Software Engineering ;)

### How are the blog posts here structured? 

I found that in the software engineering field, it’s relatively easy to pick up a lot of pieces of information that’s spread around - the internet, various blogs, going through code. But unless you build the full picture, it’s hard to put the pieces together and form a full understanding and feel like you really know it. And it’s suprisingly hard to build that full picture. Metaphorically, the things you learn are like leaves, and if there’s nothing to connect it to, it either doesn’t stick in your memory or you feel like you don’t truly, intuitively understand it. 

Each blog post here will aim to build a “tree” of knowledge for the topic that each post covers. I’ve split up each post into sections that are parts of the tree:  
**Roots** - a background to place the topic into context\
**Trunk** - core foundational knowledge - the need-to-know stuff\
**Branches** - start of some domain-specific knowledge

And with that, hopefully you’ll be empowered to go out there and build your own **leaves** on whatever piques your interest.

I'll leave this disclaimer here: I really made this to be conversational blog about software engineering topics. I may be slightly inaccurate here or there, as one might be when they're just colloquially talking to you about a complicated topic. I've just written down what I've come across and what I know in a way that's hopefully accessible and easy to digest. So please don't read this blog with a critical eye, it's simply something that I'll hope you get a lot out of. 

### How things may generally go in your early career
When you start working as a software enginner you’re usually thrown in to do a task, then another task, then another. You slowly build up a picture of your team’s systems.  Generally noone really takes the time to explain the whole system to you. No one puts the system into context. Noone encourages you to learn about industry standards. Maybe you think you don’t need to learn that stuff, you’re doing great at your job as it is. And is all that stuff really going to be directly relevant or helpful for your day-to-day job? I don’t see how it could be, you might think. If you know how your systems are set up, you’re already an expert, and you’re day to day is more based on that than this stuff. And your peers are focused on the team’s systems and day-to-day coding. You don’t forsee a situation where you or your peers will put this knowledge to use practically. 

But you know who will? The senior engineer on your team, the team lead, or the staff engineer on your team. You better believe that they have done their reading and put in their own time to learn all these things. They know where they’re day-to-day work fits into all of this, and they can speak knowledgeably about technologies that are not related to the weeds of the day-to-day work. And you know what else? Noone’s going to give you the extra time, or go out of their way to tell you that you’d benefit from knowing the background and context of the things you’re working on, much less actually talk to you or teach you about it. 

I’m happy to be the one to burst this bubble and tell you that you’re going to have to take this into your own hands if you want to be successful mid-career and beyond. Otherwise, you might still be doing well and getting good performance reviews by just focusing on your day-to-day, but you’re not going to be the one to be picked for a promotion, or to be team lead. If you’re doing well at your level, then they’ll keep you at that level so you can keep doing what you’re doing. It’s not unless you demonstrate that you have an understanding of the bigger picture, of not just your team’s system, but of the overall technology landscape that you’ll be identified as eligible for a senior role. Afterall, senior means that you’ve done your due diligence and you’re a knowledgeable person in the whole software field, not just a knowledgeable person on the team (though it is that too). Maybe you know this and you’ve tried to go out of your way to learn on your own but get discouraged by all the jargon and terminology, or you think you get it but a few weeks later you’ve forgotten because you had learned pieces of information that there was nothing more concrete to connect it to. And that’s where I’m hoping to come in.

Think of it this way: you’ll need to know these things at some point in your career anyway, so might as well get a good solid foundation of it up front to get the most bang for your buck. Once you’ve started your career on a good foot and started making contributions, really the next step to keep progressing is to form a solid big picture. A picture of how the components are connected, a picture of the technology behind the components, and an understanding of the landscape beyond what your team or even your company is using.

### It’s for me too
I’ll be honest, this blog is as much for me as it is for you. I’ve found that having this blog as motivation was invaluable to sift through the disparate cacaphony of bits of information online and distill into a story that makes sense, both for you guys and myself. We as humans are hardwired to tell and listen to stories; we have a storytelling mind. Some people say storytelling is a central part of the human experience and it’s what makes us human. To that extent, I’ll leave out links to the extent possible, so as to not interrupt the storytelling (if you’re like me, I might go down an endless rabithole clicking into the links), but I’ll add the links at the bottom. As Einstein has said, `If you can’t explain it to a six year old, you don’t understand it yourself`. I’ve created this as something that I myself would’ve liked to find and read through on a nice Sunday evening.

#### Alternate names considered for the blog:
noobsfornoobs.com (it's a play on geeksforgeeks.org, which you'll find often comes up as a top result on google when you're searching for something related to software engineering)\
onestopshop.com (self-explanatory)

```
Prerequisites:
General understanding of computer science concepts. 
General understanding of SQL.
General understanding of Client —> Server —> Database architecture. 
```

### Inspiration
The inspiration for the content on this blog was that I wanted to put out content that I myself would’ve loved to find and read about software engineering. I find tech really cool, and so many ideas in tech are so inspired and so amazing, but most of the content out there about it delivers it in a rather dry way. I wanted something that you could read through very easily, written in a way that you would think about it yourself. In this pandemic, I’ve found myself listening to various podcasts of everything from ‘The Daily’ from NYTimes to Dear Shandy from a former Bachelor contestant. These podcasts are so enjoyable and I could listen to them easily for hours on end because of the delivery and conversational tone. I wanted the same kind of easily-digestible material for software engineering.

The name for this blog was inspired by this blog: https://waitbutwhy.com/. A friend introduced me to this blog and I love it and have read every post. I wanted to bring the colloquial story-telling used on waitbutwhy to software engineering. Thanks Tim!
Some of my favorite posts from that waitbutwhy:

[Artificial Intelligence](https://waitbutwhy.com/2015/01/artificial-intelligence-revolution-1.html)\
[Procrastinating](https://waitbutwhy.com/2013/10/why-procrastinators-procrastinate.html)\
[Fermi Paradox](https://waitbutwhy.com/2014/05/fermi-paradox.html)


Now onto the posts!!

