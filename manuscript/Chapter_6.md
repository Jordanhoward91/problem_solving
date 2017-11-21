#Chapter 6 Project 5: Uber System

##Project 5: Design the Uber Ride Sharing System

Uber is a massive enterprise with servers all over the world. There are probably more applications than we even know about. With this project we're going to pick and choose some of the more visible services that Uber provides and model those systems.

You're going to build four different diagrams: an activity diagram, a package diagram, a use case diagram, and a deployment diagram. There's a reason why I picked those and in that order. It comes down to developing a mental framework for how to approach projects and different features that you're going to be asked to build.

I love starting off with activity diagrams because they provide a really nice high-level approach for how the entire system is going to work. When I'm working on the package diagram or the deployment diagram, I'll continually reference the activity diagram because it outlines how the entire system works.

### Activity Diagram Requirements

* Car ordering service process (8-12 activities)

Example Activities:

* Setting a destination
* Taking a car
* Sharing trip details

Example branching logic:

* Is the trip possible?
* Share payment with others?

Branching logic is a component that allows the system to make decisions. For example, you may check to see if a trip is possible. If it is, then you're going to send the user in one direction. If not, then you'll direct them to a different activity.

I recommend for you to investigate the different services that Uber offers, because that's what you can incorporate in this activity diagram. This is going to be a pretty large diagram comparatively. To some of the other ones we've done so far because there are so many different options that are provided in this kind of service.

After you've completed the activity diagram, then it's time for the package diagram, which will allow us to set a frame around the entire system. I want you to examine Uber's mobile application itself. That is the only package that I want you to be concerned about.

### Package Diagram Requirements

Mobile app modules and dependencies

Main modules:

* User
* Trip

Sub modules:

* Authentication
* Booking
* Payment

Nested modules:

* Single payment
* Shared payment

One of the biggest reasons to use a package diagram is when you're trying to wrap your mind around a system. You can start to see what you're going to need without getting too far into the weeds. We're simply trying to model the high-level structure.

Next is to create a use case diagram.

Use cases are primarily used to test for and model how the authorization system should work in the application. Think of real world examples.

### Use Case Diagram Requirements

Mobile app modules and dependencies

Actors:

* Passenger
* Driver
* System

Use cases:

* Search for Trip Details
* Request Ride
* Cancel Ride
* Book Ride
* Share Trip Details
* Rate Ride
* Update Payment information
* Leave Tip

Last is the deployment diagram,. I could probably spend an entire course examining how the entire Uber system could be modeled in a deployment diagram. Instead what I want you to do is model how a deployment system will work with a mobile application. It's pretty rare for mobile apps to just live by themselves. I imagine the Uber app by itself can't do anything without an outside API, so I want you to model just the mobile portion of how that system would be deployed.

### Deployment Diagram Requirements

Android deployment process with dependencies (3-4 nodes)

* API
* Smartphone device
* Android app

The more important thing is what kind of the components are needed inside of those nodes. Just as important is to define how the dependencies will work: which components and which nodes truly cannot live by themselves, and which ones need to be able to communicate in order to work properly.

##Project Solution: Uber Activity Diagram

In this lesson, we're going to walk through the solution for designing an activity diagram that shows how we can order a car using the nuber service.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Uber+Activity+Diagram+%23+1313/image1.png)

Starting here right at the very top left hand side this is going to be when the car has been ordered and we're going to start immediately right here and start with a `branch`. Now remember this is not a branch because it doesn't have a question mark here. It is not a branch that is going to have other types of places where the user can go. Instead this is a branch that simply can have multiple inputs for `set departure`. So that is just a UML mechanism and it is one of the elements that you want to have to be able to visualize how branches work and how these different activities can receive input. So you only want one item coming into each one of these activities. So the very first thing is we go and it sets the `departure`. Now from there, it sets the `destination`. Now technically you can have both these merged and I just thought that it would make sense to break them up because these are two different activities. If you have ever used the Uber app you know the very first thing that you want to do is you want to log into it when you do that. It's going to pick out where you are so that's going to set the `departure`. And so if you're building this out and this is part of the reason why I broke it into two pieces I would need to be able to find out your geo location.

This will have a full set of modules and device API requirements right here just to make sure I know where you are in where you want to be picked up. Then you also set the `destination`. And this is where you would type in the address or where ever it is that you want to go. Now with these two items, now the system can check to see if the trip is possible. So if you went into the app and this comes down to data validations if you went in the app and you're in New York City and you accidentally type a location that is in Australia uber can not take you at this moment from New York to Australia. With that in mind you do not want the system to simply plan the trip to Australia. So you need to be able to check to make sure that it's possible. If it is not possible then right here with this `branch` you want to immediately go down and give an error. And so it's going to say the price can't be calculated and it will not allow them to run it. Now you could also have a system in place where it will send the error and then it will give them the ability to start over again at the beginning. You can add that in. It's not necessary for this specific solution because I think some of these items are relatively common sense.

Now going to the next one if the trip is possible. We go down and we get the trip details. So this could be everything from the price points to who the drivers are. All of those kinds of elements. So we get the trip details and then you as a `user` are given the chance to either `confirm` or `deny` that agreement. So if you're presented with the trip details you have the ability to say yes I want to take the drive or no. If no then you're going to be redirected all the way to the top and you can start the process all over again. If you say that you do agree with the trip details then you're redirected to take the car once you've taken the car then you have some other items. And this is completely optional. But I just wanted to try to mimic the uber system as much as possible so the next branch allows you to share trip details. That's a common feature where you can send your ETA to your friends and family or whoever you're going to meet and it will send not only your ETA it will also show on a map where you are so your friends can go and track it. And I think that's a pretty cool feature.

Once you do that you have the option to `share the details` or you can choose not to. If you select yes then it's going to go down into this activity where it sends a message to the individual in your contact list,  who you want to share it with. And then it continues all along the way. If you say you do not want to `share the trip details` goes to no goes back to this branch here and then it gives you another decision to make do you want to `share the payment`?

This would be the scenario where you're going with two of your friends and uber gives the ability to split the payment up so if each one of you want to take a third then what it can do is it can go in and right here. `Choose mate to share price` so it goes in and says I want to share it with this individual. And then Ill break it up. And then finally it takes you to the process where you've had the payment approved and then you're taken to your destination.

This is a very straightforward approach to looking at the entire process. But even though there isn't a lot of complexity in this diagram. Notice how many decision points we have here. We have a few very critical ones placed at times where you as a developer or whoever is developing this is going to have to be aware that there are multiple outcomes based off of the data input such as is the trip possible? Does the individual agree with the trip that's proposed? Do they want to share trip details? Do they want to share payment? Each one of these is going to change the logic and it's going to change the flow of that user's experience and that is one of the biggest key's is with building this type of activity diagram. Now I really like these kinds of diagrams because I could take what I have right here and it would help me go and visualize exactly how I would organize the code base. And that leads us into our next solution where we go and we build that package diagram.


##Project Solution: Uber Package Diagram

In this guide we're going to examine the solution that I implemented for the uber package diagram.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Uber+Package+Diagram+%23+1314/image1.png)

Now, once again this is most likely going to look very different than what you've personally built out but I want to walk through the way that I personally like to think about it so that you can use it for your own types of diagrams. And one the key components that I want to stress before we even get into the solution is the way that I personally like to think about `package diagrams`. Packages are what I like to construct before I touch code. This is essentially my whiteboarding experience this is where I go in and I start to list off the types of features and modules I know I'm going to need to build into the system. I can't translate this directly into code but I can use it to be able to get me to that next step and so that is really what `package diagrams` are all about.

For example starting up here in our `user module` the user module I know is going to need to use several items. So I have an `artifact` here called `use` and that's perfectly optional. You don't have to put it there but the reason why sometimes I like to do it is for these diagrams as they become more complex the association and what it represents becomes more important. So here there is a very big difference between a module that uses another module compared with a module that simply has access to one of the other modules just like we have between the `trip` and the `user`.

This does not denote a deep level of dependency or coupling. Instead it simply says that this `trip module` here needs to access the `user module`. It still is a dependency because a trip cannot happen without users. However the main and primary objective that I want to focus on is that the trip can access the user.

Now let's go down the tree of everything that the user module needs to use. It needs to use `authentication`. This tells me I'm going to have to build in a way for users to log in and securely check to see if they are who they say they are. They also are going to need a `profile`. So I know I'm going to have to keep track of data such as their rating and to be able to see a historical list of all of the other places that they have been. And then also because one of the best benefits of using Uber is that you don't have to manually enter your payment information each time the way you do with a taxi. The `payment module` is going to be nested inside and the `user module` is going to use that `payment module`. And then from there the `payment module` is going to have its own set of nesting.

This is something that I really wanted you to focus on when it came to building out this diagram is figuring out exactly how you could integrate nesting. Because for example having a single and shared `payment module` should not directly be accessible by the `user module`. These are items that should only be used directly from the `payment module` because essentially a single payment is a type of payment and shared is also a type of payment. So our `payment module` is simply going to use these items.

That doesn't mean that we have to use inheritance or any thing object oriented It simply is referencing that this `payment module` needs to have access and needs to use the code inside of these libraries.

Now moving on to the next set of modules and our `trip module` we have already mentioned that it needs to be able to have access to users. So this is going to give us the ability to perform tasks such as finding who the user is if they're logged in successfully. If so then you could perform tasks such as seen their destination and seeing where they're starting from. Now some of the other items that need to be inside the `trip module` one it needs the ability to import an `SMS gateway`. So if you are sending any kinds of text messages or anything like that which uber allows then the `trip module` needs to have access to that code. Now you may wonder why did I not just include `SMS gateway` inside and said I want to be able to use of this. And part of the reason is that this comes down to a code structuring kind of decision. I do not want to use the `SMS Gateway`. I actually just want to import this library so the rest of my system can use it.

Now that may seem very subtle and it is. And that's perfectly fine if you didn't use an artifact like this in fact it's probably rare for anyone to do that. But I wanted to include it in here because myself as a developer would most likely have included this as an import statement because this is a third party library. So I would be importing this I wouldn't be creating it from scratch. Now if I continue down the stack to see what exactly the `trip module` needs to use. Well it needs to use `search` and search could mean many different things it could be searching for a destination it could be searching for a point of interest an address and so this would be relatively vague because a number of details would have to be added to it. And then also I would need the ability to have some type of `booking engine` so this would be a module that would connect and would pass my trip module details in here so it would keep track of where I started from what my destination was going to be and then it would perform all of the tasks associated with booking that ride.

Now, Uber is much more extensive than this. If I were to build out a package diagram for the entire system it would be pages and pages long. The core functionality that I wanted you to build in was what you would imagine designing if the creators of Uber came to you before it was a system and they just told you some of the basic user stories you could be able to create a package diagram like this and that would give you a starting point on building out the rest of the application.


##Project Solution: Uber Use Case Diagram

I really enjoyed putting this diagram together specifically because it does a very nice job of showing not only the functionality of the application but also how users should be interacting with this.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Uber+Use+Case+Diagram+%23+1315/image1.png)

Remember that `use case diagrams` give us the ability to build our entire authorization system. Now also note authorization is different than authentication authentication. Is the system that allows users to log in securely. Authorization, shows what types of features and components that a user should have access to. Now here we have three actors we have the `passenger` actor we have the `driver` and then we have the `system` itself. Now a passenger has the ability to interact with every one of the listed components. You can go down the line all the way from `search for trip details`, `requesting a ride`, `canceling a ride`, `booking a ride`, all the way through `leaving a tip`. Now the driver only has access to a few of those use cases.

A driver has to be able to `book a ride`. And when I'm saying Book ride what I mean is not book a ride with another driver but they need to be able to interact when a passenger is requesting that ride so that they can say yes I would like to accept that. So they're going to have to have access to that. Now with uber, uber drivers also have the ability to `rate the right`. So Uber lets their drivers not only drive but also say if the experience with the passenger was good or not. So that is a use case that's actually shared by both drivers and passengers. It's a pretty basic set of use cases for the driver.

Now let's look at the system itself. Now when a passenger says they want to search for trip details that's going to interact with the system. So there's going to be some type of `Geospatial` type of search engine that occurs and that is going to be what the system is in charge of the passengers to type in an address and the system is going to return back what the potential route would be along with any of the details such as the estimated time of arrival and anything else that the user needs. Now when it comes to the passenger requesting a ride the system needs to be able to interact with that as well. Now technically you could say that the system is in charge of everything here and that's the reason why I added this type of distinction where this is not the system as a whole. This is the `navigation engine`. So just to be clear on that the system is going to represent what is being managed from a navigation perspective. So every time a passenger `requests a ride` that needs a `navigation component` every time the passenger `books a ride` that needs a `navigation component` as well. Because if you've ever taken an uber you know that as you're on your journey the system is constantly updating your little dot and showing you how close you're getting to your destination. Now the last item here that I'm going to discuss is this `cancel a ride` use case. So this is something that you may notice that nothing directly has access to canceling this ride.

The reason for this is because even though canceling a ride can be performed by the passenger it needs to have a ride to cancel first. So this may have been different than what you implemented in your own solution and that's perfectly fine if you drew a line between the passenger actor to cancel a ride that would still be valid and you're definitely not going to get any points marked off for that. But I included this because this is an important if not subtle kind of difference to show that the process of canceling a ride is dependent on a ride being there to cancel.

Each one of these other items has the ability in a sense to stand on its own. So sharing trip details. This one is going to be able to live by itself whereas `cancel ride` that is going to be happening while the request process is occurring. So when you request a ride during that time you have the ability to cancel this. Now once you have booked the ride you can no longer cancel that. And so then it just keeps on going down the line.

Now there are subtle differences with each one of our solutions. I'm already very confident about that. And that's perfectly fine. This is also going to on your own experience and your own knowledge of the uber system the main components I wanted you to focus on is building out a system where one actor really interacts with pretty much every component in the entire system. And then you have these other actors that can add functionality just like we have with our navigation engine system and with our driver.

##Project Solution: Uber Deployment Diagram

In this lesson, we're going to walk through the solution for building out a deployment engine.


![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Uber+Deployment+Diagram+%23+1316/image1.png)

And specifically, we're going to see how we could build the deployment engine for the Android app that Uber uses. Now technically this could also be very similar to the iOS application. The main components that I want to really talk about and the main nodes that I want to model deal with mobile versus a desktop system the Uber architectures so massive we probably couldn't even build it if we dedicated an entire course to it because it is made up of thousands of different applications that all have their own specific rolls and behavior. So what I wanted to do was pick out a type of architecture that is very common to have to build out which as if you're in the development industry you're most likely going to have to learn how to build out and model systems that work with mobile apps and so that's what this is going to focus on. So starting off on the right hand side. So we're going to get everything here on the left in a while. But right now I want to talk about the Android app as it relates to its data layer. Now with out an `API connection` there is no Android app. Uber cannot have an Android app that lives by itself. So one of the biggest components is needed in order for this to function properly is the `API`. This is where when you search for a user or you search for a location or any kind of outside data comes into the system its hitting this `API` and its returning a response.

So in the middle we have this node called the `device` which is going to be the smartphone. This is where the entire application is going to live. And then we have a connection and this association between the `execution environment` which is Android. Now if we were building this for iOS applications then we would have an iOS execution environment and part of the reason why this is important is because these types of systems are very different. So if we were to simply create one deployment diagram for both mobile apps then you're going to run into a number of problems and they mainly revolve around the fact that Android uses the Java programming language which has a completely different set up than iOS uses. IOS uses swift and objective c.

In order to have your applications run they are very different. The environment that you use to set them up is very different. The deployment processes are incredibly different in regards to deploying either updates or deploying to the App Store for the first time. I've performed both kinds of deployments and they are completely night and day. Google is very easy to deploy to if I perform an update in an Android app that I have then within a few minutes it'll be live on the App Store. If I do the same type of change to an iOS app it may be days before the update goes live. So all of that goes in the decision making process on modeling these systems out.

So we have our `device` we have our `API`. We know that the `execution environment` here is going to be Android and then we have a connection to that deployment engine.

So here we have our `node` which is the `Android app` itself which is an Uber app and we have a number of classes resources and these are going to be both compiled and uncompiled. If you're wondering what the difference is and why I wanted to separate those it's because Java is a compiled language. And so what that means is that your code itself is going to be compiled. However it does deal with data that does not compile so data that comes in from the API usually comes in in the jason format that's not compiled it's simply dynamic data that runs through the system. So it's important to understand that you have two different kinds of processes in regards to the code that is there in the app and then from that point we have our deployment specification. What this typically means is that we place in the system the different updates and we list out the changes that have been made to the application. We change version numbers we do a number of tasks. Kind of like a checklist. That's the reason why it's here.

Now, I want to point out that this is a very generic system. We don't know the code base that the uber team uses. So all we can do is estimate based off of what we can see from the outside. And so this is incredibly high level. My guess is that the system that you built out is probably completely different looking than mine and that's perfectly fine.

The main components that I wanted you to be able to model in this type of system is having some type of mobile application and recognizing that it does rely on an `API` because this app would not be able to live by itself. It needs to be able to have its own execution environment it needs to be able to dictate what type of phone this can go on and then from there the data can be pumped through. So this is one option on how you can model a `deployment engine` for the uber Android app.


![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Uber+Deployment+Diagram+%23+1316/image1.png)

And specifically, we're going to see how we could build the deployment engine for the Android app that Uber uses. Now technically this could also be very similar to the iOS application. The main components that I want to really talk about and the main nodes that I want to model deal with mobile versus a desktop system the Uber architectures so massive we probably couldn't even build it if we dedicated an entire course to it because it is made up of thousands of different applications that all have their own specific rolls and behavior. So what I wanted to do was pick out a type of architecture that is very common to have to build out which as if you're in the development industry you're most likely going to have to learn how to build out and model systems that work with mobile apps and so that's what this is going to focus on. So starting off on the right hand side. So we're going to get everything here on the left in a while. But right now I want to talk about the Android app as it relates to its data layer. Now with out an `API connection` there is no Android app. Uber cannot have an Android app that lives by itself. So one of the biggest components is needed in order for this to function properly is the `API`. This is where when you search for a user or you search for a location or any kind of outside data comes into the system its hitting this `API` and its returning a response.

So in the middle we have this node called the `device` which is going to be the smartphone. This is where the entire application is going to live. And then we have a connection and this association between the `execution environment` which is Android. Now if we were building this for iOS applications then we would have an iOS execution environment and part of the reason why this is important is because these types of systems are very different. So if we were to simply create one deployment diagram for both mobile apps then you're going to run into a number of problems and they mainly revolve around the fact that Android uses the Java programming language which has a completely different set up than iOS uses. IOS uses swift and objective c.

In order to have your applications run they are very different. The environment that you use to set them up is very different. The deployment processes are incredibly different in regards to deploying either updates or deploying to the App Store for the first time. I've performed both kinds of deployments and they are completely night and day. Google is very easy to deploy to if I perform an update in an Android app that I have then within a few minutes it'll be live on the App Store. If I do the same type of change to an iOS app it may be days before the update goes live. So all of that goes in the decision making process on modeling these systems out.

So we have our `device` we have our `API`. We know that the `execution environment` here is going to be Android and then we have a connection to that deployment engine.

So here we have our `node` which is the `Android app` itself which is an Uber app and we have a number of classes resources and these are going to be both compiled and uncompiled. If you're wondering what the difference is and why I wanted to separate those it's because Java is a compiled language. And so what that means is that your code itself is going to be compiled. However it does deal with data that does not compile so data that comes in from the API usually comes in in the jason format that's not compiled it's simply dynamic data that runs through the system. So it's important to understand that you have two different kinds of processes in regards to the code that is there in the app and then from that point we have our deployment specification. What this typically means is that we place in the system the different updates and we list out the changes that have been made to the application. We change version numbers we do a number of tasks. Kind of like a checklist. That's the reason why it's here.

Now, I want to point out that this is a very generic system. We don't know the code base that the uber team uses. So all we can do is estimate based off of what we can see from the outside. And so this is incredibly high level. My guess is that the system that you built out is probably completely different looking than mine and that's perfectly fine.

The main components that I wanted you to be able to model in this type of system is having some type of mobile application and recognizing that it does rely on an `API` because this app would not be able to live by itself. It needs to be able to have its own execution environment it needs to be able to dictate what type of phone this can go on and then from there the data can be pumped through. So this is one option on how you can model a `deployment engine` for the uber Android app.
