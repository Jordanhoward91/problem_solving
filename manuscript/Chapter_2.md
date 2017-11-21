#Chapter 2 Project 1: Build Twitter

##Project One: Design Twitter System

Welcome to Project One, where we are going to build and design Twitter.

I want to make a very quick point, because you'll hear me say "design" quite a bit throughout this course. When I say "design" I do not mean building the user interface. That is a *completely* different course. That's when you're building the way that the users are going to interact with the application at a very high level and a user interface perspective.

When I say "design", I'm talking about how the system is architected. As a developer, when someone says that they want you to "design the system", this is most likely what they're talking about.

This project will involve a two-pronged approach, using both structural and behavioral UML diagrams.  

Now, for the structural approach, we will be using class diagrams. These are the types of diagrams that can pretty much be translated directly into code. They allow you to set up your database associations and list out all your attributes, method names, and so on.  

In order to complete this project, you will need to build a

* user class
* tweet class
* retweet class
* preference class
* security class
* message class
* hashtag class
* reply class
* like class
* location class
* image class
* users to follow other users

When you build this diagram, each one of those classes is going to represent its own database table, and it's going to be its own entity. You'll need to list each of the attributes inside each class. You can use Twitter for guidance, but build these classes in the way that you think is best

As far as operations within the application go, remember, those are method names. It might be "post a tweet" or "show a tweet" or "get all tweets". There's all kinds of different method names that you could use, but each one is flexible. You do have to use the full list of classes that I just gave you, but there is flexibility in regards to the attribute names and the method names and how all of those work. Imagine that you are the developer that they tasked with building Twitter, and take it from there.

I want you to pick out all of the class names and attributes that you think make the most sense, and then, most importantly, I want you to set up the relationships between them. For example: a *user* can have *many* tweets, which is implementing multiplicity. Show how that association works.

Each one of these classes is going to be connected in some way or another to another class. Not one of these is a standalone entity, so that's a very important concept to keep in mind.

Next are the behavioral diagram, which will involve building a use-case diagram. Remember that use-cases are very high-level. They're a great way of visualizing the types of authorizations that users have.

The different use-case diagrams are going to be for:

* Actors: User and Follower
* Posting tweets
* Retweets and Likes
* Optional features (e.g. Images to posts)

I want to leave the optional features up to your own creativity.


##Project Solution: Twitter Use Case Diagram

Welcome to the solution for the Twitter project.

Now, each one of the solution videos in this course is going to be broken down into its own individual guide. The reason is because there are a few goals that I want to accomplish with the solutions. One is definitely so that you can have something to compare with what you've already put together in your own project. So, being able to check and see if what you built is similar to what we have here.

The other reason, though, is because when you're out in industry, when you're working on your own real world development projects, I want to give you guides that you can reference. For example, we're going to talk about a use case diagram in this guide. And so in your future projects you may want to be able to come back and look and see what the correct syntax and structure is for a use case diagram. So you can come back and look at one guide instead of having to sift through a number of them. So with all of that being said, let's jump into this first solution where we walk through a use case diagram for building the Twitter functionality.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+1%3A+Twitter/Post+Tweet+use+case+diagram.PNG)

Here we have two actors. We have an author and we have a follower. You can think of an author as someone who authors a tweet.

Now, remember, your solution does not have to match all of the elements that I have because I want you to be able to use some of your own creativity and didn't want to lock you down into a set of requirements where you weren't able to explore what your own solution would look like. Here, we do have two actors though, because we want to have someone who is going to write tweets, and then we're going to have someone who can follow those. That's one of the most core fundamental types of features that Twitter makes available.

So let's walk through what an author can do in this use case diagram. They can write a tweet. As you can see, we have this "Write a tweet" use case and inside of "Write a tweet" there are a number of items that this includes. Writing a tweet might be something where they write a tweet from scratch. However, they also will be able to retweet a tweet. They can also like a tweet and they can also send a message. This would be such as forwarding a tweet. So this is some of the functionality that is wrapped up inside of the "Write a tweet" use case.

Now, we also can get into the ability where we have an extension on this tweet. If you have used Twitter at all you know that you can write a regular tweet that just has some text content, but you can also upload an image to the tweet and have that shared. So that's why we have a metaclass of `<<extend>>`. It's extending the functionality of the tweet where you can attach an image to a post.

We additionally have this follower actor. So what we have to do in modeling out this use case diagram is build in the type of functionality where we want to be able to show what one actor does, and then also the types of use cases and the type of functionality that one of the other actors is going to have. And so in this case let's see what a follower can do.

A follower can write a tweet, they can retweet tweet, they can like a tweet, and they can message. Now technically this is a very basic kind of use case here, because an author and a follower are technically interchangeable. If you're following another user, then you're still an author. Every user on Twitter is an author and that's a reason why the functionality that you have as an author extends to every one of the use cases.

The reason why it's important to have this secondary actor here is because we need to be able to see what a follower has access to. Imagine a scenario where we're not rebuilding Twitter but we're rebuilding, say, Wikipedia, where different users can also edit posts. So not only would they be able to write their own post, they could also go and edit a post. And so you'd have other functionality for the secondary type actor. Now, Twitter doesn't have that functionality so we didn't build it in, but that's why it's important to include all of the various actors that are going to be interacting with a specific use case.

Now, when I was originally learning about UML, I would usually run into a couple problems. One is that I'd make a system overly complex, where I would go in and I would take a very simple process and then I would build way too many actors, too many use cases, too many extensions, too many includes, and the system would be very hard to read. And then there were also times where I would oversimplify things and I would not have the right kinds of connections.

One thing that I want you to do is to be able to learn from this solution. If you fell into one of those camps where you made something that was overly complex or you made something that was too simple, don't worry, that was exactly the way that I did it. The only way you're going to learn how to build out an effective diagram is by trial and error and being able to work through problems until you find the right balance. Remember, the goal is, and this is what helps me now in building these, is being able to think of the core functionality that the application needs. This gets a little bit into user experience but also into how the code should be structured. And so the goal of this is, if I were to hand this off to a developer, or if I were to take this and write the system myself, I want to build it in a way where I can look at this use case diagram and in just a few minutes be able to take this and then start to build a framework in my mind for how the system should be modeled.

So nice job going through the use case diagram portion of this project and in the next guide we're going to dive into the class diagram.


##Project Solution: Twitter Class Diagram

Welcome to the solution for the Twitter class diagram.

Now this is going to look very similar to what we implemented in the UML training course, if you went through that, but I made a number of modifications. And the main reason is because I didn't want to give you the full answer to the project and so this is a slightly modified version that has all of the same class names but I made some changes that I would personally use in a project if I was tasked with building Twitter.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+1%3A+Twitter/Twitter+Class+Diagram.PNG "Twitter Class Diagram")

Now there is a lot of content here. This is definitely one of the larger class diagrams that you'll go through in this entire course, but this is great training because this is a pretty standard kind of setup for building an application. There are some important components here that I want to point out. There are also some optional elements here that I want you to be aware of because there are going to be many times where an organization has their own version of UML. They have their own type of syntax and their own way of doing things. And that's perfectly fine. I write my own UML slightly different than any other developer that I've met. There are always going to be slight changes. And so what I want to do is point out what the standard elements are and then show you why I've made some of my own creative decisions, because they work for me.

Let's start off with the tweet class.

Now I'm not going to go through all of the attributes for every single one of the classes. Like I mentioned in the instruction video, this is something that I'm leaving up to you based off of what you personally have discovered when you've researched Twitter. But just for this one we'll mention that there are elements such as an ID, text for the tweet, a reference to who the author is, if it was retweeted or not, when it was created, and different elements like that. You may notice that I don't have the data types for each one of these. Usually, I'll only put the data type when I feel like it's a custom one that really needs to have some additional explanation. For example, I know that `text` is going to be of type `text` or a `varchar` or something like that. Being able to add that in there doesn't really make the process of development any more efficient. So I don't like spending time on things that have no real benefit. And so that's just one example and you'll see that throughout this entire course.

And that's a reason why if you asked 10 developers and software engineers who are experienced in using UML and you task them with this project, you're going to get ten different variations of that project. That's one reason why I want to show you what some of those types of variations are, because when you go to work you're going to experience that, and I don't want you to think that there's only one right way of doing things.

Now with all that being said, there are some elements that really do need to be inside of every class diagram, so we'll focus on those. One of the most common is being able to demonstrate multiplicity. Remember, multiplicity is the practice of being able to show how an association is going to be defined. So our tweet has the potential to have many "likes." If you go to Twitter and you look at a tweet, you will see that it does have the ability to have multiple people who have liked that tweet. In our diagram, you can see that a tweet has many Likes and the way that that is defined is with the association arrow, and we have "1" followed by a star. What that means is that one tweet has the ability to have many likes.

Now there are many elements of a class diagram that are optional. However the one part that I'm going to stress is to make sure that you have your multiplicities correct. The reason for that is if you were to hand me a UML diagram and say, "Go build an entire database based off of this diagram," if the UML multiplicity items like this are set up properly it's going to make it very easy for me to go and build out all of those models, because I'm going to know that each like is going to have to have a reference to the tweet. So that's going to be a foreign key relationship right there. If this is set up incorrectly then what's going to happen is it's going to cause more problems for the developers. They're going to build it out and then only later realize that they had to have a foreign key inside of like. And so if you're passing this off to another developer they're not going to like you very much if you do not set up that component because you're creating more work for them.

Now, remember, inside of any type of class diagram, you have the name, followed by the attributes, followed by any operations. Typically, in my own approach, I don't spend a lot of time adding the names of the operations. And the reason for that is because it's been my experience that it just creates a lot of boilerplate work--in other words if I'm building out a `new()`, a `create()`, an `edit()`, and an `update()` action inside of a class then I already know as a developer that I'm going to add those in. It would just waste time in adding them in at this stage. I'll usually just throw in some of the operations that may be slightly different than standard ones, just to give myself or the developer that I'm handing this off to an idea of some of those custom components.

But one thing that I do think is very important is to list off the correct attributes, because what I will do as a developer is, when I take in a class diagram, I will go and generate my models based specifically off of this list. So I'll go create a tweet model that would automatically have an ID, but I would say it needs a text, an author reference, a retweet reference, a created, a like, hashtag, etc. etc.. And so that is something that I would literally copy and paste those elements and those names into my own generators. So I spend more time thinking about the right way to set up these attributes and less on these types of methods.

So that is tweet and like. We're not going to go over every single one of these elements because you're going to notice there are some incredibly similar types of components, so I want to focus on what makes them different. And then you can always reference the master file if you have any questions about any of the other components.

Now one of the types of syntaxes that I use that is different than the UML specification is for join tables. So, if we look at say the TweetHashtag table or the Retweet class, what these are is--they're not as much classes. Depending on your programming language they may be *called* classes, but what they really are are join tables. So, in this case, a tweet is joined to a hashtag class via this join table. And the reason why I like to use this dotted line syntax is because UML is visual and that's the entire point of the language. So if I am looking at a class diagram I like to be able to know where my classes are, like tweet, or like, or image, or hashtag, and I like there to be some type of clear visual distinction between those classes and the database tables that join those classes.

In other words, TweetHashtag is not going to have any operations. It's not going to have a set of methods. All it's doing is allowing me to have navigability between a tweet and a hashtag. If you remember what navigability is, it allows me to look up a tweet and then run a method that goes in and queries all of the hashtags. So that's what the TweetHashtag class allows me to do. And whenever I'm designing a system, if I know where the join tables are, I know that that's going to help me make several decisions.

One of the first and most important decisions is it's going to tell me that I can't create this class in this database table until the tweet class and the hashtag class have been created. That may not sound like a big deal, however, it actually is, because this tells me the order that I need to build each one of these models out and that I know I'm going to have to create a tweet class before I can do this TweetHashtag one just because it has to have a reference to a tweet *and* to a hashtag. So that's definitely one key reason, but then it also is simply helpful to understand that the functionality inside of these types of elements is going to be very minimal. It simply is a way that we can join classes together.

Now, for a tweet to retweet, this one's a little bit different because this is what's called a self-referential table. What we're doing is, we don't want to create an entire class for retweets, because, if you think about it, a retweet is simply a tweet. So this could be something, if you really like using inheritance, you could do something where retweet is a type of tweet, and then that would be able to give you access to it. But in the case of the way I typically build out systems I would simply make this a join table that can reference itself so that I will know which objects are tweets and which ones are retweets, simply based on what is inside of this join table.

And notice how this has a reference to retweeted, so, which item got retweeted, along with the new tweet that got created. So, in other words, to take a practical example, if I'm following a friend I see them make a post and I click on the little retweet button, then it's going to generate a new retweet record in the database that's going to have a reference to my tweet along with the source one that was retweeted. And another option that you could have added in here is "content," because Twitter in later years gave the ability not only to retweet but also to add notes associated with it.

That's another nice thing about using join tables, is they are not only there to keep track of IDs, they can also keep track of additional content that brings those together.

There is one other element I want to focus on and that is "following."

So we have our user class. It's pretty basic. It takes in an ID, name, time zone, city, and then some security settings, and then it has this following element. Now this is something that is very tricky for junior developers, and so being able to understand the way this works is going to help you out a lot when it comes to either going out and getting a job or building this type of functionality into your system. And this is not just for social networks. It's definitely something that you'll need to use if you're building out a social network, but at the end of the day there are very few applications, especially large production applications, that don't have to have this self referential kind of set up in some form or another.

We can see that we have our following join table, and we have users. So the tricky part here is we have a user that needs to be able to follow another user. But how do you keep track of that? Having this type of join table is a great way of doing it. So, if you have User A who wants to follow User B then what you can do is create this database table and be able to say, this following user is where we're going to store the ID of who is being followed. And then we have follower. So we're going to store the user id of the person who is performing the following action. And the nice thing about this is, because we have this reference right here, and a user hasMany followings, and following hasMany users, we can run clean database queries to perform actions, such as being able to render a list of all the users that one user is following.

And you're also able to perform tasks such as being able to create a feed. If you've ever wondered about how, when you're on Twitter, and you have all of these various tweets coming in from people you follow, it's accomplished using this type of setup. And what it's called is a self referential table. Notice, we're not joining items together. If you've never implemented this before I definitely recommend for you to research the concept of self referential tables but then also go and implement it in code and be able to learn how that works. This is going to be something that you're probably going to have to implement at some time or another.

So those are some of the key elements that are included in this solution. I definitely recommend for you to explore the entire source file and be able to see the way that I implemented it. And just like every other solution in this project, yours is going to look different than mine. It needs to have the same core components, it needs to have the full list of class names, and, in this case, one of the most important things is really focus when you're analyzing this and comparing it with your solution, focus on these multiplicities. Focus on those to make sure that you have the table set up correctly, so that you know which table and which class hasMany of another element, and when you have items such as when a class belongs to another class.

Remember the point of this entire course: to give you the ability to solve problems. Wwhen you're tasked with building out an application, and especially if it's a non-trivial type of app, that can be a very scary thing if you try to jump into the code right away. What this course is aiming to do is to give you an in-between step to be able to say, let's take a step back and let's model the system so that we can understand what we need to go build. Because the smaller of chunks that you can break a problem into the easier it starts to become. So by building out a properly structured class diagram, what you're going to be able to do is take this diagram and instantly convert it into code, you're going to be able to go and build your entire database just based off of everything that you put inside of this diagram.
