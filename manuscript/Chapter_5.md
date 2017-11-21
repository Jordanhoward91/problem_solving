#Chapter 5 Project 4: Enterprise Fleet Management System

##Project 4: Design an Enterprise Fleet Management System - Part 1

Welcome to the Fleet Management project.

A fleet management system allows a company to manage their fleet of vehicles, as well as many other types of things. In fact this fleet management system started out with a project that just the fleet manager was using. Once the CEO saw it, he liked it so much he started using it for the entire company to manage their assets and to work with maintenance.

Most of the time, you're going to be asked to build something and you're not going to have a clear picture of what needs to be done. You're going to be given a set of requirements and then you're going to have design a system off of that. That's what we're going to be doing in this module.

One of the biggest takeaways from this course is how to develop your own mental model and framework for planning and designing a system. I want to take you through what I would do, because, at this stage, it's a very vague project. They want a way of being able to maintain and keep track of all of their vehicles. There's not a lot of detail.

In this project, you're going to build four diagrams. I want to start by looking at the behavior, so we'll design an activity diagram first.

I want you to model in this is the entire process of maintenance. This should include between 8 to 12 activities.

### Activity Diagram Requirements

* Maintenance activities (8-12 activities)
* Start point: Maintenance Inquiry
* End point: Maintenance Complete

Example action items:

* Technical diagnosis
* Assign service member
* Order parts

Make sure that you have decision points, guards, and the other elements that are required inside of a activity diagram, so that it can have dynamic behavior. Use your creativity, and think about the different requirements for the situation.

The fleet manager didn't give me a list of requirements. He said that he wanted to keep track of his vehicles, service records, maintenance logs, parts orders and so on. If you're working with someone who's not very technical, then it can be incredibly helpful to spend some time modeling the behavior. This gives them an opportunity to look at the flow and decide if what you're building will suit their needs, or if there are more requirements that aren't being addressed.

After finishing your activity diagram, I would keep a high-level view because we're still trying to develop a complete understanding of the project and its requirements. We'll move to a package diagram next, but avoid defining any classes.

With a package diagram, I can model out all of the main modules that the system's going to need, and then I can model the different operations associated with each of them.

### Package Diagram Requirements

Fleet management modules, operations + dependencies

Modules:

* Personnel
* Vehicles
* Parts
* Maintenance
* Partners

Think about how these modules might operate inside of a system that is designed to manage a fleet of vehicles. Then, think about how these modules might relate to each other. Last, include some operations specific to each module. It's still too early to be very detailed, so keep your approach high-level.

For the vehicle module, for example, you might include some type of buy/sell operation to be able to manage how you're acquiring these vehicles. That was important when I built out the original fleet management system. They needed to know when a vehicle was purchased and how much it was purchased for, because that dictated how much money they were willing to spend on maintenance.

A very important point when it comes to building out any kind of system is to keep your approach as straightforward and as practical as possible. It's very easy to involve complex computer science concepts in our modeling, but what I've found is that I'm much more successful when I simply try to put myself in the shoes of the person I'm building it for. Whether that's the end-user, or various members of the organization, at this stage I simply try to figure out what would make this program most helpful to the business.


##Project 4: Design an Enterprise Fleet Management System - Part 2

The third diagram that we're going to build out is a deployment diagram. This helps us figure out the overall architecture of the system. I want you to research what an enterprise system is comprised of. There are some complex components.

### Deployment Diagram Requirements

* Load balancer
* Application servers
* Database clusters
* Caching

We haven't gone over these topics in any other course so far. When you're designing systems you are constantly going to be designing things you've never built before. For that reason, a huge component of the planning stage is *research*.

So find out what a load balancer does! You don't have to go build one yet, just figure out what it does at a high level.

We started this project with an activity diagram, where we figured out the behavior. That informed our thinking and helped us to have an idea about the different classes.

With the package diagram we saw how all the modules could be set up and how the system could talk to itself.

The deployment diagram gave us a good idea of the overall architecture.

With all of that in place we're ready to build the class diagram which will lead us directly into building the application itself.

### Class Diagram Requirements

* Vehicle
* CarModel
* CarBrand
* ProductionFacility
* Dealer
* Technician
* Role
* Maintenance
* MaintenanceType
* ServiceCenter
* Service
* ServiceList
* MaintenancePart
* Part
* Vendor
* Assembly

From a technical perspective, a few of these classes could be combined into one. But in more complex enterprise applications it becomes incredibly important for your database to be as efficient as possible. A great way to do that is to make sure that classes do not contain information that they do not need.

You can choose whether to use inheritance for this diagram, or to simply specify that there are multiple models; one is more generic and another is more specialized.

As always, make sure that you put in all of the right types of associations, attributes, and operations that you think you would use. Finally, be sure to list which items are public, private, and protected.


##Project Solution: Enterprise Activity Diagram

In this lesson we're going to walk through the solution for the fleet management activity diagram.

This is going to focus on the process of tracking maintenance, which has a number of activities that we want to be able to visualize. But as with most activity diagrams one of the most important parts of this entire model is giving us the ability to check to see what happens when things don't go right, and being able to visualize the branching logic on when we expected one thing to happen but something else happened. That's really the point of pretty much every activity diagram that we're going to be using in this entire course.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+4%3A+Enterprise+Fleet+Management+System/Maintenance+activity+diagram.PNG "Maintenance activity diagram")

Our start point when a user has some type of maintenance inquiry. So imagine that you want to give truck drivers the ability to say, "I think there might be something the matter with my truck." Or it may just be time to go in for regular maintenance on it, such as an oil change or new brakes or something like that.

We first have to go through this technical diagnosis checkpoint. So right here we want to be able to have one activity where there's some type of review process.

Remember, the whole point of each one of these projects is to focus on specific types of behaviors that you would build, not just in a system like this, but in many other types of systems. So imagine that you're building some type of work flow management type of system where you have users that can submit requests, such as saying that they have an expense and they want to be able to get it paid back from the company. You're going to have this type of step where we have a first line of technical diagnosis where the data gets run through a process and somebody, some type of admin, or some user on the system, has the ability to see all the data, and then from there they can pass it to the first set of the branching logic.

Next, it's checking to see can it be fixed right now. If it is some very quick issue that doesn't require a lot of work then we send them straight to the maintenance step. We have one other QA process where we make sure that everything works, and if so then they're on their way. That is the easiest scenario. In my experience this very rarely occurred. Usually it couldn't be fixed immediately, so it got branched into another type of process.

Next, we have an activity "Assign service center/team member". This is a common activity in a lot of systems.

Further along, we have "Perform detailed technical diagnosis." Now this is different than "First line technical diagnosis," which is a high level diagnosis.

The reason I'm going into detail on these activity diagrams is not because I think you're going to be tasked with building out a fleet management system. What I'm wanting to impart more than anything is to show the level of detail that you want to build into the system. You want to have enough activities in here that it matches the level of functionality that's going to have to be built into the code base.

After it's checked for the detailed technical diagnosis, it checks whether new parts or assembly are required. If no, then we can move to booking a technical specialist. If parts or assembly *are* required, then it's going to book those required parts. It'll check if those parts are in stock or not. If not, then it's going to have to order those from the vendor. After those are restocked, we'll be ready to book the technical specialist. If the parts are in the system and they are available then it can go straight to booking the specialist.

From there, it follows down into the last activity where we check to see if we performed the maintenance. If the vehicle is OK, we're ready to go. If not, it goes all the way back up to the detailed technical diagnosis.

Now this goes back to what I said at the very beginning of this guide one of the most important components of building an activity diagram is not the best case scenario. If that was the case, we would simply be able to take it from a maintenance inquiry, to performing the technical diagnosis, and then take it to maintain. However that would be missing some very critical components that have to be considered when building out this type of feature.


##Project Solution: Enterprise Package Diagram

In this lesson, we're going to walk through the potential solution for the fleet management system package diagram.

When I built the system, I was able to break it in to these five modules. Remember one of the most important elements of a package diagram is being able to show the dependencies. If you did not build your system to have the proper types of dependencies I recommend to look back at your project and see how that can be cleaned up a little bit.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+4%3A+Enterprise+Fleet+Management+System/Fleet+Management+System+package+diagram.PNG "Fleet Management System package diagram")

Starting on the top left hand side we have our Personnel module. This is going to track drivers, the admins, etc. We have the ability to hire, to leave, to have authentication, and to log out. These could be users of the system, and they may also be truck drivers who may not have to log into the system.

When it comes to analyzing the dependencies, remember that a dependency doesn't just mean that we have to be careful about removing certain modules. It also means that Personnel can access Vehicles but Vehicles is not going to access Personnel directly. So dependencies also represent the access levels that these modules have between each other.

The reason why Personnel has a dependency on Partners and why it can access Partners is because only a user has the ability to add a contract or delete a contract, and Personnel is where all of our users are. So that's a module in Partners that the Personnel Module needs to be able to access. And so that's why this particular component has to be able to communicate with it and why it also depends on it personnel. Does that make any sense. Living by itself if it is not in this scenario going to be communicating with the vehicle module and with the partner module. Now technically you could create a system where the Personnel Module does not have those same types of dependencies. So imagine if you built a system that had authentication as its own application and it worked among all kinds of different applications. So I built a system like that where it did communicate with a enterprise fleet management system and then it communicated with an asset management system and add all of these different apps that it could pass users through and so you only had to log in to one app but it could go and could communicate with all of these other ones. In that case there isn't that same level of dependency because Personnel can live by itself. But in this case we really care about how the users can interact with partners with vehicles and so on and so forth. That's the reason why those are represented that way.

In Vehicles, you can see that we have a few actions such as being able to assign, maintain, buy, and sell. From there, the dependencies and the access points are that a Vehicle has to be able to have some type of communication with Parts. And the reason for that is because you're going to have this entire library of parts in the database and the vehicle is going to have its own set of requirements. Anytime you use a phrase such as "needs access to" that means that there is a dependency there. So our Vehicles need access to our Parts catalog. And just like that, vehicles also need access to Maintenance.

The Maintenance module is the entire process of being able to start, finish, and then maintain the supply of all of those various elements required to build this system out.

One thing that I also want to point out to you is that we have Parts and we have Maintenance. Now technically, Parts is going to be able to be translated directly into a class and a database and that's where you're going to be storing all of your types of items. Maintenance is very different. This is not going to just be a database class with methods. This is going to be almost like a miniature application in itself. It's going to have a number of classes and modules and helper methods all built into this system. It's going to have its own workflow just like you saw in the activity diagram. So that's something that is a very important point when understanding how to construct package diagrams is just because you have two components that look the same that does not mean that they are going to have the same type of behavior or that you're going to be able to translate that directly into code.

This is part of the reason why package diagrams are the diagrams that you build at the very beginning of your project. It's your way of being able to brainstorm and create some type of organization for how you want to structure your code base.

Let's move to our last module: Partners. Partners can provide information to Personnel. That's a reason why personnel needs to have access point to it. But partners needs access to the Maintenance module, because partners are going to interact with the supply system, and they're going to have to pass back which parts they have in what quantities. If you look back at the activity diagram, this all goes back to that one sequence where the system checks to see if a product is available and then it can perform ordering.

Now this package diagram is much more complex than our phone parser one. And for very good reason that application was much smaller than this fleet management system. And in actuality this was the first draft of the fleet management package diagram the one that I ended up building is much different and much larger. I didn't want to show you the complete and final diagram because I didn't want you to think that I had gotten it absolutely right the first time. No one knows the kind of system we're going to build until we actually start getting into it. If it was possible to construct these type of UML diagrams perfectly before touching the code then you wouldn't really need programmers. All you'd need is a set of computers that could read these diagrams and then go build the system for you. Instead, the whole purpose of these models and these type of diagrams is to give you a head start. It's to give you the ability to take a set of requirements and users stories and all of those types of components and structure them in a visual way so that you are able to get a little bit closer to actually building the system.


##Project Solution: Enterprise Deployment Diagram

In this guide, we're going to walk through the solution for the fleet management systems deployment diagram. I mentioned that there are a number of components inside that I wanted you to research and include, as a refresher.

The reason is because every project that you come into and that you're asked to build is going to propose some unique challenges.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+4%3A+Enterprise+Fleet+Management+System/Fleet+Management+System+deployment+diagram.PNG "Enterprise Deployment Diagram")

Starting with the load balancer, I went with one of the most basic options here,k which is a 50 percent traffic split. This means that if I get two requests then the first one I'm going to be sending to the first application server and then the second one I'm going to be sending to the secondary server. So if User A comes in when they go the Web site the load balancer takes that traffic and redirects them here. User B hits it right afterwards and then they are sent here and

The whole point of using a load balancer is pretty much like it sounds. You want to balance the load of traffic so that you're not so dependent on one system. The other nice benefit is if there's some kind of fault with this application server, and it goes down, then this other server can take all of the requests.

There are a lot of details that go into building a load balancer. This is a pretty straight forward implementation. You have to perform checks, such as a response from the application server to make sure it's running okay, and so on. Right here, I'm performing a pretty basic structure where we have a 50 percent load going to one and 50 percent going to the other.

So how are these application servers able to serve identical content and pages to the user? A lot of it comes down to the cache cluster. What caching allows you to do is to be able to save references and other components either on the user's system or on your own server. This is a critical component when it comes to improving the performance of applications. A lot of frameworks will do some of this work for you. For example the Ruby on Rails framework has caching built into the system for items such as CSS stylesheets and Javascript. For more advanced applications you usually have to perform some type of caching by yourself.

There are a number of services, such as Cloudflare or Amazon AWS that allow you to do this. I usually put my cache cluster on a third party service. I'll have them store my assets, my HTML, and the like, because those items are not going to change on a regular basis.

I also have the ability to make the cache expire. For example, I may push up a change to the server and then I may forcefully expire this cache so that it pulls in the new version of those files. This is especially useful if I made changes to the CSS styles or the Javascript. That's just a very high level overview of how caching works.

Lastly, we have our database cluster. Part of the reason why I structured it this way is because this is a pretty common pattern. You want to be able to cache certain items that are not changed on a regular basis--usually view-centric items--however, you don't want to cache data. Imagine a scenario where you have a user who wants to go check the status of their maintenance request. If you cache that maintenance request then that record is not going to update for them, even if someone went in and *did* change the status. So it's very important to understand which items should be cached and which ones shouldn't. Usually the way that I will run something like this is anything that changes on a regular basis I'll place inside of the database cluster and then I will not perform any caching on that.

I want to be clear that, just because I usually reference caching for HTML/CSS/JS assets, there still can be some level of caching that's related to data. On that side, you just have to make a decision on what data changes on a regular basis and what you want to give your users access to.

Great job going through that project. Hopefully now you have a better understanding of how load balancers work, how caching works, and how it can be applied in a deployment diagram.


##Project Solution: Enterprise Class Diagram

In this lesson, we're going to walk through the class diagram for the fleet management system. Unlike some of the previous guides where we walk through the solution for the class diagram, this one doesn't have a lot of surprises.

Essentially, is a CRUD based application, which means that you have a number of tables and then you have the ability to make changes. Like I mentioned in the requirements video, the main element I wanted you to focus on is the concept of breaking out tables into smaller tables, because when it comes to building an enterprise level application, you really want to make sure that you're building well-structured relationships.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+4%3A+Enterprise+Fleet+Management+System/Fleet+Management+System+class+diagram.PNG "Enterprise class diagram")

The Parts and MaintenanceParts classes are a great example. You can see that this could be accomplished in a few different ways. Technically, MaintenanceParts is a type of Part, so this could be subclassed, but just because you have the ability to use inheritance does not necessarily mean that you should or that you need to. It just comes down to personal preference.

The main type of behavior that I like to model inside a class diagram is my database. This is where I can set up my associations and break my tables up into as many pieces as I need. For example, could we have connected Parts directly with the ServiceList? Technically yes. However, what happens if the fleet management system does really well and they want to start adding the parts that they use when they're going out to perform their work. If we ever needed to start adding in the list of parts from the inventory for their other services, that would not fit inside of MaintenanceParts. We would have to go back and create another class for their other types of parts. By separating this out what we can do is allow our system to be more scalable in the future.

There's only one other element that I want to focus on in this diagram because we haven't really seen it too much: a one-to-one relationship. I've personally worked on a number of projects where this type of construct of having a one-to-one relationship was one of the most helpful things in regards to how I set up the system. The reason for that is navigability. For example, we can call a Vehicle object and then just ask, "What car model are you?" I can just call a Vehicle and it's a direct navigation point to the CarModel class.

There are many times where I've seen students who thought that every relationship had to be either a one-to-many or a many-to-many relationship, and I think part of that is because it's probably the most common kind of set up. However, there are many times where you do not need to have a one-to-many relationship. Because of that, you can clean up your entire codebase because it's much easier for one object to communicate with another object.
