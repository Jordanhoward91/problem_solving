#Chapter 8 Project 7: Marketing Automation System

##Project 7: Design a Marketing Automation System - Part 1

Welcome to the final project in this course. In this project we're going to build out a marketing automation system. At a high level this system is going to allow an organization to track and communicate with potential leads throughout the sales lifecycle.

A great example of this is something that we use for our Bottega code school. The user signs up and they say that they want more information about the school. That triggers what we call a "journey", where they communicate with different specialists along each stage of the cycle. This could be for more information about pricing, the curriculum, the experience, and so on. The journey ends when they sign up for the course, or express that they're no longer interested.

This system will also communicate with outside services, such as Salesforce for customer management, Twilio for sending messages, or even HipChat and Slack.

As always, we're going to start off with our most high level diagram: a Use Case diagram that outlines the entire behavior for the system.

This is slightly different and more advanced than we've done in the past. Usually, we use our Use Case diagrams to outline what roles each actor has, but in this one I want to stretch it out build a diagram that would serve as a starting point if we wanted to get straight into the coding.

### Use Case Diagram Requirements

Actors:

* Marketing Specialist
* Lead / Customer
* System

Use cases:

* Marketing Specialist
  * View Reports
  * Manage Contacts
  * Manage Forms
  * Send Communication (email, SMS, HipChat, Slack)
* Lead/Customer
  * Submit Form
  * Notify Marketing Specialist (automatic)
* System
  * Send Reminders
  * Send Special Offers
  * Send Communication (feeds in)

A key component to this system is that only the marketing specialist will be interacting with the system itself. The leads won't interact with the system at all, they will only receive various forms of communication.

Now this is one of the more complex parts because we have concepts like "Send Communication", which can mean many different things. It could be an email, an SMS, or something else, so we'll define that.

Moving down the line, we're going to build another behavior diagram.

We have a few vague concepts here, so we're going to take a look at the high level behavior and the experience we want the user to have. In this diagram, we'll model the entire journey process.

### Activity Diagram Requirements

Marketing journey flow (8-12 activities)

* Start point: User filling out a form
* End point: User purchasing

Example activities:

* Welcome Email
* Delay 1 week
* Marketer Notification

Example decisions:

* User purchased product?
* Was email opened?

Research:

* Fork nodes
* Join nodes

We're going to place decisions throughout this system because it's very dynamic. It needs to be able to change state and redirect users based on feedback. We wouldn't want to hardcode the flow.

Imagine there's a customer that signed up on day one. You don't want to send them marketing messages a week later asking them to sign up. Another example decision might be checking to see if a user purchased a product, or if an email was opened, which shows if they're interested or not.

Also, spend some time researching fork and join nodes. We haven't discussed either of them so far, so figure out how they could be incorporated into this diagram.

With our first structural diagram, we're ready to start putting the journey modules in place and organizing our dependencies.

### Package Diagram Requirements

Journey system (5-6 packages)

* Journeys
* Insights/Reports
* Channels and App drivers (Slack, HipChat, SMS, etc.)


##Project 7: Design a Marketing Automation System - Part 2

Our fourth diagram is going to be a deployment diagram. For this, we want to focus on how the APIs are going to be connected, because there are a lot of moving pieces in this system.

### Deployment Diagram Requirements

* Load balancer
* Multiple application servers
* Database cluster
* Email server
* SMS Connector
* SMS Provider
* External CRM

We're modeling a system that plugs into tools like Salesforce, and then lets you follow a lead as they're taken through the marketing journey. You'll have the ability to track what that data flow looks like with this diagram and see where the servers are positioned.

I included a load balancer again so that you can review how that can be diagrammed, but the big focus on this diagram is the API connectors. You'll need nodes to connect the system to various outside services, such as Salesforce or the SMS service. Feel free to get creative with how you organize these, because this is a very complex system. You're going to have servers all over the place, advanced systems like load balancers, and even services you don't even own, which is a very common practice in modern development projects.

Our fifth diagram is a state machine diagram.

### State Machine Diagram

* Visitor
* Prospect
* Lead
* Opportunity
* Closed (Won)
* Disqualified Prospect
* Unsuccessful Lead
* Lost Opportunity

The user's state is critical when it comes to modeling a system like this. We have to keep track of what type of user we're dealing with, because that helps us decide what actions we're going to perform.

For example, a potential customer will start as a "Visitor". They can then become a "Prospect", "Lead", and "Opportunity". Ideally, from that state, they will be marked as "Closed (Won)", which means that they actually became a customer, but there are other possibilities. We also have to take into account whether they are even qualified to be prospect. If a 12-year-old signed up for devCamp we wouldn't be able to enroll them as a student, so that would immediately disqualify them. Maybe they tell a marketing specialist that they're just not interested, which makes them an "Unsuccessful Lead". Lastly, we have a "Lost Opportunity", which is a situation where someone went all the way through, but at the very end they decided they did not want to sign up.

Being able to capture each one of these states is vital, because the state is going to determine how we're treating that customer at any point in time.

Last, but certainly not least, is the class diagram. The focus here is going to be on inheritance.

### Class Diagram Requirements

* User
* MarketingRep
* Report
* Form
* Journey
* Reminder
* Message
* Email
* SMS
* ExternalChannel
* Customer

Focus on how we can create a generic class, and how we can leverage subclasses to get more specific.

The Message class in particular can help us understand how to model inheritance, because "Message" is something that's generic. No one's actually going to *use* a message. They're going to use one of the more specialized Message *types*, such as email, SMS, and external channels.

A simple way to tell if you're using inheritance right is if you would describe one class as a *type* of another class. For example, an email is a *type* of message, or marketing rep is a *type* of user.

Finally, remember that a customer is not a user. They do not interact with the system, so we need to keep track of them in a different way.


##Project Solution: Marketing System Use Case Diagram

In this lesson we're going to walk through the potential solution for our marketing automation system. Now as I mentioned in the requirements less and I really wanted you to extend yourself on this use case diagram.

Usually when I'm building our use case diagrams I'm focusing on the permissions and I'm building a tool that will let me build my authorization system. But here I think we can take it a step further and we can get even closer to what the implementation is going to look like. In this particular application gives us a really nice opportunity for doing that.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Use+Case+Diagram+%23+1321/image1.png)

So first let's take a look at each one of our actors. We have a `marketing specialist`. We have the `system notification engine` component of the system and then we have a `customer`. One of the most important elements of this diagram is being able to integrate an actor who is never going to technically interact with the system itself at least in the traditional way. The only type of action and use case that the customer is going to do is they're going to submit a form. After that the dialogue the communication.

All of those elements are going to happen outside of the system. And from that point it's going to be only the `marketing specialist` who is interacting with us. If we think of a real world use case this would be like a potential customer going and typing in a contact form on a Web site from there that kicks off a process where it notifies the `marketing specialist` and it's perfectly fine if you included these types of artifacts such as include here I do those simply because I want to give myself a little notation to let me know that in this submit form I'm going to have to include this module this `notification module`. But if you did not have that in there it's still perfectly valid UML. So following the chain of events after we've notified the `marketing specialist` from there it goes and it starts sending the communications out.

Now sending communication can mean many different things for this type of system. It might be an email it might be an SMS it might be some outside service like hipchat or slack and we need to be able to take all of that into account. Whenever I have a system that needs these type of extensions where it's one action such as sending a message but that action may have to get visualized and may have to happen in many different formats than what I typically do is I create this type of wrapper module like send communication and then all of the other `actors` all the other use cases can interact with this one use case and then it can be in charge of routing traffic to whatever outlet it needs to go to. So it's going to send communication. And that may be an email, SMS message, or anything like that. And the `marketing specialist` also has this kind of communication layer. Now I'm going to get into him at the very end.

Let's moved to the `notification engine` what it is in charge of is sending special offers sending reminders and the cool thing about building a system like this is we can leverage this communication module, so it's not just how a `user` is interacting with the `marketing specialist` and vice versa. We can use each one of these communication components for other things. Since this is being modeled on a real world application that we're currently building out I can give you a really good example of how this works. Not only will a lead start the communication chain but also we're using our notification system to do tasks such as sending out these type of offers. So if we have a restaurant that has a number of people who have signed up they can go and the notification system can send SMS messages to their users promoting specials such as happy hour deals or coupons. And even though this communication module in this sense is usually used for managing leads it can also be leveraged for all kinds of other use cases so that is something to keep in mind whenever you're building any type of system whether it's say an image uploader many times an image uploader can also be a file uploader for PDF's and Word documents in with the proper software engineering you can build your systems to become much more scalable so that one module has the ability to perform many different tasks not by itself we still need to follow our good design patterns but what it can do is wrap up and extend itself. And that's the reason why I added these extend types of `artifacts` here to show that these elements these are going to have to be modules possibly and applications all by themselves but they're going to interact with this send communication type of process.

Now lastly coming to the `marketing specialists`. They're the ones who are going to be interacting with the system the most. So they need to be able to view reports, manage contacts, manage forms, and then lastly as we've already mentioned participate in this entire communication chain. So this is something that is a little bit different than some of the other use case diagrams we've built up until this point. And it is a very important type of diagram to understand mainly because there are going to be many times where you do have to build use cases where you have one `actor` such as we have with our `customers` here who has limited system interaction. But you still have to model what those interactions are going to look like and how it fits in with the rest of the system.

And then secondly the most important thing that I want you to take away from this particular solution is how you can visualize some type of abstract wrapper like we have here with `send communication` so that you can build your systems in a way that they're scalable and that they're flexible.


##Project Solution: Marketing System Activity Diagram

In this lesson, we're going to walk through our activity diagram solution for our marketing system.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Activity+Diagram+%23+1322/image1.png)

Now, this is going to have a few unique components that we haven't integrated into any previous activity diagrams and they are definitely very important especially in modern development architectures. And if you remember I said that you needed to research `fork nodes` and `join nodes` and I have added notes right here to show what those represent. And we'll talk about them more in detail but these are definitely very important elements to add whenever systems start to get more complex and we'll talk about how that really plays out once we get to this point.

Let's start at the beginning. This is where a user fills out the registration form and this triggers the event of a welcome email. Now this comes to our first fork node. And so what a fork node represents is that we have one activity that actually branches out and causes two other items to happen in this case it means that we have a `delay of one day` and then we have a `marketer notification`. So this essentially means that after their welcome email it's going to go into the queue. And there's going to be a one day delay before anything happens and then the marketer is going to be notified. Now why this is important for modern types of applications is because most of the apps that you'll be building will need to have some type of background processing. So that's a development mechanism that allows for a system to perform one task and then perform other tasks in the background.

And so right here we're performing a few different kinds of tasks. We have a marketer notification. So this is an email an SMS, whatever the marketer chose to get for their notification that lets them know that a user filled out a form, then it goes and it triggers another process where we have a delay in where any of the other actions are going to occur. Then we come to a `join node`. So what this represents is we might have a few different activities but then they come back together. So they're happening at the same time and then they come back together in this joint node and then everything continues on just like before. So those are the two most important items I want you to understand in this type of diagram. I'll give you another good example that's outside of what we have here with our marketing automation system.

 I've built out a number of machine learning algorithms and many of those can be very slow very server intensive. And so it's not possible to just run those simultaneously along with all of the other types of tasks that are running on the system so what I have to do is build out a pretty complex background jobs system where it can go and when a new record comes in it goes in the background and it performs all kinds of the machine learning tasks. Some of them take a few split seconds others take a few minutes and so it can be a pretty long and tedious process.

And the way that I always visualize how that occurs is by using these fork and join nodes so that I can show that certain tasks can and might even have to take place at the same time. So after those two activities have been joined together we are taken to this first decision point and it asks was the welcome email opened? And so that's a pretty important thing from a marking perspective because if someone signs up but never even opens up the email that you send them then that means that you might need to change the way that you're communicating with them. So if it was opened then we're going to come down and it's going to delay one week before it starts the rest of the workflow. If the email was not open then it comes to this other branch here and it might perform a few different tasks. It's going to send a special offer email but then it is also going to come down and check to see was a special offer email opened. And so that is essentially it's the same thing we did here except it's on a secondary e-mail. If yes then they get redirected to this decision point. If no then they're going to contact them a second way. So if they filled in their e-mail and their phone number then it's going to come down and it's going to send an SMS message on their phones and say we have some discounts. It's going to delay one week so both ways we are going to get this one week delay in the automation process remember the whole point of this system is it's supposed to create these kinds of marketing funnels also called marketing journey's.

It's where you can set these entire little mini sales adventures essentially where you can dictate when the delays occur how you want them to be notified what happens when certain tasks occur such as opening an email or not opening one. And then no matter what happens you are taken to this branch right here. And then we check to see after all of that after we had them interact with the system after we sent them SMS messages regular e-mails. Did they buy something? If they did then we take them to the end. We're not going to continue to send them marketing material if they have not bought something then we delay a week and we take them all the way through the entire journey again and we'll keep on sending promotional materials and those kinds of elements.

Now I did not add in a secondary endpoint which is kind of a common sense thing so that's a reason why I didn't add it in. Which is if someone unsubscribed then that stops the journey entirely. So you definitely could put another End Point Inside of say this little area here and it can say something like "Did the user unsubscribe?" If so then their journey has ended as well. But I didn't feel the need to do that because nothing actually has to happen in the system. Besides for a basic unsubscribe process the more important element is what we have here which is following them all the way from when they filled out the form all the way till they purchase. And then also building in the ability to have this looping process occur until they have made a purchase.

##Project Solution: Marketing System Package Diagram

In this solution, we're going to walk through the package diagram for marketing automation engine.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Package+Diagram+%23+1323/image1.png)

Now this is going to be a relatively straightforward package diagram. The most important component here is I want to show how to visualize communicating with outside services. So as you can see we have our frame right here called `package marketing automation`. And then inside of it we have a number of packages we have `journey's`, `insights`, `channels` and then inside the channels we have `app drivers` and then we have nested components here where we have a `slack` package and then a `hipchat` package and then we have this `aggregate` type of association description. And the reason for this is because technically slack and hipchat are going to be outside services and they need to implement whatever we have here for our outside app drivers. So what I typically like to do in a situation here where I'm going to be passing messages to outside services such as slack or Hipchat or Twitter or Facebook. Each one of those systems has their own unique API.

If I were to simply build one module that was supposed to communicate with each one of those that would start to lead into some very messy code. What I try to do instead is I create one connector that can manage all of the data communication and then other elements so other packages such as slack and Hipchat and this instance can then implement what we have with app drivers and so I can communicate with any one of the outside services but the journeys and all of the other parts of the application they won't even realize that theyre doing it so it doesnt care if its sending a message to slack or SMS or any other type of communication channel.

All it knows is that it's communicating with this app driver module so you can send a message, a user, anything like that. And then this driver can be in charge of handling all the API communication. Communicating in a way that is secure getting responses back and it can manage all of that inside of the package and that's really one of the most important parts I wanted you to get out of this entire solution is how you can wrap that up.

Now as far as looking at some of these dependencies journeys is the main functionality of the application. If you went through the solution for the activity and the use case diagram journeys really is the focal point. This is what happens when a user signs up and starts going through the entire marketing automation system. Now through that journey also needs to be able to communicate and have an association with insights. So in order for the journey to function properly it has to know when the last communication with a user occurred. It needs to know if a user opened up an email or responded to a text message. All of that data is going to be stored inside of insight. So in that case journeys does have a dependency on insights. Now journeys also has a dependency on channels because a journey is all about sending out communication. It doesnt manage the actual sending of it but it is in charge of managing everything that leads up until that point.

So a journey isnt really able to do anything if it can't communicate. So in that case a channel is definitely a dependency for journeys. And so this is a pretty high level diagram but it should give a good idea on how you could wrap an entire system, a entire marketing system up and how you can illustrate what the dependencies are and also how you can nest packages inside of other packages.


##Project Solution: Marketing System Deployment Diagram

In this lesson, we're going to walk through a potential solution for the marketing automation systems deployment diagram.

Now, this diagram is going to encapsulate a lot of what we've learned throughout the entire course because there are all kinds of different components that need to be integrated in order to have a system like this function properly.

Notice that we have multiple calls to the Internet. Whenever you see this in a deployment diagram it means that you're most likely interacting with some type of API or you're showing how the direct communication is going to happen with a user like we have right here. So starting here in the top left-hand side we have a user who's going to make a request. We clearly show that that request is going to come through the Internet and that may seem like a straight forward kind of thing to say. However, there are plenty of times where this might be, not a user but some other API or something like that.

And if you come down here that's actually what we have here and that's part of the reason why I have this little computer used as an icon and this is perfectly valid UML deployment diagrams are some of the most visual types of diagrams that are out there because there are many times where, as you can see these different nodes all look very similar. But whenever you look at the user you can tell that that is someone's computer with their desktops so that very quickly shows that this is going to be a user who's just working on their computer sending requests.

Now that's different than what we have here. This is an outside user it's an outside client that is going to be interacting with the system using the Internet. But this is going to be something like sales force and this is an integration that we've built in with the marketing automation system where we can communicate with sales force and update different records in the sales force database based off of how the journey is and how all of the different systems on the marketing automation side are happening now moving down after we have that. All of that communicates with a load balancer it doesn't go straight to the servers it has to communicate with the load balancer first and that is going to dictate how the traffic is going to flow. So the load balancer is going to split up the traffic. And in this case, we're still just using two application servers. However, this could be stretched. You could have this stretched over five or 10 servers if you have a massive application and the load balancer can manage all of those processes.

Now each one of these application servers is also going to communicate with a shared database. So right here we have a database cluster.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Deployment+Diagram+%23+1324/image1.png)

We have our D-B master and then our D-B slave. And so if you are familiar with how databases work especially in architectural level then you know that the D-B master is what these application servers are actually interacting with and then the slave is your replication system so you can have your database backups and you can make sure that if your DB master goes down then it can be instantly replaced with this slave.

Now, this is a pretty standard setup for load balancers. Each one of these application servers is going to have the identical code. And because it's interacting with the same database right here then the user experience is always going to be the same. Now moving down these are going to use an e-mail server which is going to be a separate service I'll use services such as Sparke post or send grid and those kinds of tools. And those are not inside of the servers. They make API requests to that outside service. And then this email server is in charge of processing all of those e-mail requests. And that's a reason why I have use because we're using this service and then continuing down with that same pattern. The system also needs to communicate with an SMS gateway for the applications I work on that require SMS. I usually integrate Twilio, and Twilio is a great tool that allows you to send SMS messages via API calls. So our application servers are going to interact with the email system with the SMS gateway and if you also are going to extend this even further it can use all other kinds of systems so you could extend this to use slack, to be extended to use hip chat to all kinds of other outside services and they would just continue down the line.

Now the last component here is this SMS gateway is going to use the Internet so it's making an API call and then that's going to be what is going to communicate with this provider. Now the way that we have it set up we don't have the application servers directly interacting with Twilio.

Instead we built a wrapper for that so that each one of the servers can send custom messages and it doesn't have to worry about the Twilio API at all. It simply sends it to this SMS Gateway and then it handles all of the processing. It's an application that stands by itself and it handles 100 percent of the processing for communicating with Twilio. And the really nice thing about this is if you're building out a system and say that you did integrate your Twilio or any API connectors right inside of the app server code if one of those providers say Twilio decides to change the way that you need to communicate with the application with their system then you'd have to go and change your core code you'd have to alter the code base just to make it change to fit in with Twilio's changes.

And that's really considered a poor practice. You don't want your system to go down just because Twilio decided to make a few changes. So from an architecture perspective what I like to do is I like to create some type of gateway a type of wrapper that I can have 100 percent control over the system. I can take better care of having custom error messages if Twilio does change or if there's a outage on their side and then I can communicate that much more clearly to the servers and to the code base as opposed to relying on them to do it. So I'll usually create some type of wrapper many times like in this case it is a standalone API only application and then these apps simply communicate with it.

It manages all of the connections between Twilio and then Twilio will send back all of the data when you get a response. And then obviously it is in charge of sending those SMS messages directly. So that is a marketing automation systems deployment diagram that includes everything from outside API calls to tools like Twilio and sales force and also how you can configure a load balancer.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Deployment+Diagram+%23+1324/image2.png)


##Project Solution: Marketing System State Machine Diagram

In this guide we're going to walk through the potential solution for our state machine diagram for a marketing automation system. Now, this is something that is very critical in a system like this.

One of the most critical components of a system like this succeeding relates to how well it can manage the state. Imagine a scenario where you have a visitor who comes to the site they fill out a form and then you start sending them all of these marketing automation messages. And then they decide to purchase or they say they're not interested or they're not qualified. And for some reason, the system doesn't manage their state properly and you keep on sending a message as that would be a very bad experience and in fact, it's actually illegal. It's illegal to send messages to users that have said that they do not want to have messages. That's a part of the Spam Act. So it's very important in cases like this to be able to properly manage how the states work. So this is a little bit larger of a state machine diagram and we're going to start all the way up at the top.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+State+Machine+Diagram+%23+1325/image1.png)

Now notice that this may look very similar to an activity diagram. However, if you look at each one of these states these are very different. They are not activities they're not actions. They represent a state not what the user happens to be doing inside of each one of these Decision Points. This does represent an action and then that will affect how the state changes.

 So in the very beginning whenever you have a start point that goes straight to a state that means that that's the beginning state. So we have a user who starts off as a `visitor`. Now if they `submit` the form then they move down if they do not submit the form then it simply goes back up. And it means that their state has become `unchanged` and this is not just related to a marketing automation system. Imagine building a state machine diagram out for a social network. If you have a user who's not logged in and not registered then that user as they travel throughout the entire application their state will remain as a visitor.

So if they do submit the form though then it comes down and they are now a prospect. So their state has changed from visitor to prospect. And then we check to see are they qualified for the CRM conditions. This would be a scenario such as checking to see if you only sell to individuals in the U.S. and the U.K. and you have someone from Australia then that means that they are a disqualified prospect and so you would simply change their state so that it is a disqualified prospect and unless something changes then they would simply stay in that zone. Now they always can change it so they can update it say that you all of a sudden now do accept sales from Australia. Now this would come down here it would ask the same question and we would move down the line. So after they've been qualified they are now in the state of being in the `lead` if they are a lead and they get moved down. It checks to see are they qualified for a CRM opportunity condition.

This could be something like saying that you have all of these different items that need to be checked. A very easy one would be saying that it's a law that you cannot have anyone that is under 18 years old signed up. So this would be checking something like that in the CRM. Now technically what we have here(Qualified your CRM conditions) and here(Qualified CRM opportunity condition) could be merged into two processes. The reason why I'm showing this is because this layer right here this is a very initial check. And so you may not be able to even get a lot of information from the user at this point. So all you'd be able to maybe do is find out what country they're in or some basic information like that. Once they become a lead they'll fill out a card or some type of some type of web component where they give more information. And then once we have that information it gets processed through the CRM. It checks to see are they qualified with our more advanced types of qualifications. And if no then they are an unsuccessful lead. They stay in the state unless something changes. If they do qualify then they come down and they're no longer a lead. Now they're listed as an opportunity in the opportunity State. There is only two different options that can occur. The first is that they come all the way down and they talk to a sales person and if they say they are not interested then they will be a lost opportunity if they purchase and they say they are interested then the opportunity has been won and their state has been closed and has won.

This is a very important component when building out a system like this. I like to make sure that each one of these States represents the same participant. Notice this is not the state of the system it's not the state of other users it's not the state of the marketing engine or the employee. Instead this is representing only the users state. And so that is a very important part of building out a state diagram that is effective and also is easy to read because you can look at it and you don't have to worry about what state visitor is verse unsuccessful lead and which type of user that represents. It's just very clear right here. Any one of these diagram components is representing the state of the user.


##Project Solution: Marketing System Class Diagram

In this lesson we're going to walk through our marketing automation systems class diagram and many of the components you will see here are going to be the same types of elements that are in most class diagrams

It's very good for you to go through those because the more practice you have with them the more familiar they're going to be and then it's going to be pretty much second nature when you're building these out yourself.

Now, this combines many of the different components that we've learned throughout this entire course. You may notice some things such as multiplicity here and there are also some very unique forms of it that we haven't really integrated before such as right here. We have a one to many type relationship but this is an interesting one usually our one to many things are usually one two and then an asterisk but right here I'm doing one to zero dot dot.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image3.png)

And what that means is that a form can exist with out a set of customers. And the reason for that is a pretty straightforward one. If you remember back to our process a marketing rep can create a form. So as soon as they've created that form it is LIVE. It's on the site but no one's actually filled it out yet. So in that particular state there is a form. So we have one but it does not have any customers that are related to that. So whenever you're writing your multiplicities make sure that you're building those in a way that they just follow common sense kinds of patterns. And so it's a very common way of doing it.

I also wanted to show a little bit different way of denoting it compared with how we've done in this course so far. Many times we'll just do one two and asterisks but I like to, in cases like this where there is a potential that there could be zero of an item, I like to be explicit with that there are many times where it's going to be one to one dot dot asterisks. And what that would represent is that whatever that relationship is and as it exists it needs to at least have one. So this would be a situation where say a marketing rep created a form but it wasn't actually a full valid form until there was a customer associated with that so they'd have to add a customer to the form. And in this example, that really doesn't make sense but there are plenty of times where you do need to be able to have a one to one or more type of relationship so that that's one very important part of the solution. I want you to review and focus on.

The next is really in how inheritance can work inside of these class diagrams coming down to message,

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image1.png)

we have our message class right here. And this is our wrapper for our entire communication system. This is going to have a customer id the assigned representative. All of those different attributes and a message though may be many different things. A message might be an e-mail, an SMS message, or some other external channel such as slack or Hip chat or Facebook or Twitter or any other connector that you need.

Now the reason why I like this type of implementation is because a message is a parent class and then an email is a type of message, SMS is a type of message. One of these external channels. Is a type of a message. My rule of thumb whenever I'm deciding if I want to implement inheritance inside of some type of application is if I can describe it and I can put the class names in a sentence like that where it can where one class is a type of another class that is one of the most traditional and pure forms of a time where you want to use inheritance an email by definition is a type of a message each one of these are. And so this is a case where utilizing an inheritance or some form of it definitely makes sense.

The last element that I want to mention is a reference to our customer class here.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image2.png)

Now in many different applications usually a customer would be connected to user but in applications where the customer is not actually a user. So in other words they do not have a username and password they're not logging into the system or any of those tasks all the tasks that a marketing rep needs then the customer is just a standalone class. This is someone who signs up on one of the forms and we need a way of tracking them. So we obviously need some type of database record for that customer but they're not going to be a user. And that's a very important distinction because if you built this and said OK we have a user abstract class and then customer inherits from it and so does marketing rap.

That would be a poor way of structuring your system because a customer is not a type of user. If you explain what a user does a user is someone who logs in the system with the username and password which you can see all of those different elements right here.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image4.png)

A customer does none of those things, and so because of that a customer would not be a good fit for inheriting from user. A marketing rep, on the other hand would be. And if you're wondering why I created two different classes we have a marketing rep and a user.


![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image5.png)

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image4.png)

There is a very important reason why. And I like to structure my systems like this is because 9 times out of 10 when I build a system even if the stakeholders say there's never going to be any other type of user except for a marketing rep 9 times out of 10 that's not accurate. At some point someone's going to say you know what we need an admin or we may eventually want the customers to be able to log in and there can be all kinds of different users. That happens constantly and because of that just based off of years and years of experience I now always separate my user types out so that I can prepare for when that happens. So yes marketing rep technically is a user and that's a reason why we have, noticed in the multiplicity we have this one to one relationship.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Marketing+System+Class+Diagram+%23+1326/image6.png)

That means that every user is only going to have one marketing rep and vice versa.

The reason for that is because at some point there is most likely going to be some type of site admin or some other type of user that needs to be created and instead of just log jamming the entire set of requirements and behavior for that other type of user inside of the User class I can simply have it inherit from user and then have a clean interface for that other type.
