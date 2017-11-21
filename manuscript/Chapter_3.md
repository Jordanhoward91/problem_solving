#Chapter 3 Project 2: Coffee Ordering Application

##Project Two: Design an Ecommerce Application

In Project Two, we are going to build an Ecommerce system, which you will probably have to do at some point in your development career. In this case, we're going to build an online coffee ordering system.

One of the most common questions that I get from students is how to build out some type of Ecommerce  platform, which is why I added this project to the course. You'll learn how to build all of the different components and structure them so that they can relate to each other. This will give you a high-level view of everything that's required.

In Project One, we built out a social network. Social networks, in general, have a very complex design. They have to have things like self-referential tables, joined tables, etc. which gives them their own unique set of complexities.

Ecommerce systems, on the other hand, have their *own* set of complexities. This project is even more complex than the Twitter project, with its own set of features and its own design.

One of the key differences I want you to focus on in this project is the HasMany and BelongsTo relationships. For example, the Order class is going to "have many" products in it, and it's going to "belong to" a user. With the Product class, that Product is going to "have many" line items. There are many different ways that you're going to have to implement parent-child relationships and discover how to model that nesting in the best way.

In addition to a complex data model, this type of system also has a number of challenges around building out the behavior. For this, we're going to utilize an activity diagram where we outline every single element and every stage that a user is going to see from when they enter the site all the way through to a completed purchase.

### Project Requirements

We're going to build two diagrams. The first one is going to be structural, and it's going to be another class diagram. Expect to build a diagram that is about 10 to 20 percent bigger than the Twitter project.

#### Classes

* User
* Address
* City
* Country
* Cart
* CartItem
* Inventory
* InventoryItem
* InventoryOption
* Taxonomy (or, Category)
* Relationship between inventory and taxonomy
* Payment
* CreditCard
* PayPal
* PaymentStatus
* Order
* OrderStatus
* OrderItem

Now, let's talk about the activity diagram. We need to cover a full flow from: when the user gets to the application, all the way to when they've purchased a product.

#### Activities

* Search
* View based on categories
* Viewing Products
* Customizing products (update qty, style, etc)
* Add to cart
* User registration
* View cart
* Update cart
* Checkout
* Payment

Make sure to include validation points throughout the process. For example, what happens if their credit card comes up and is declined?


##Project Solution: eCommerce Activity Diagram

Welcome to the solution for the coffee ordering service activity diagram. Now this is a very important activity diagram to be able to understand, so if your system ended up being very different than this solution, then I would definitely study it quite a bit.

Not because I believe it's the perfect example, but because this is a very common process that developers need to model. This is the concept of building e-commerce into a system and depending on what type of job that you're in this is probably going to have to be built out at some point or another. This is an activity diagram that I personally would be able to take and it would give me a very nice visualization on the functionality that I need to build into the system. Not just from being able to track a user going from page to page, but really one of the biggest takeaways for this project is to be able to visualize what happens when things don't go right.

It's very easy and it's one of the most natural things for us to do, is to build out a system like this where we just imagine everything working. But the problem is, when we do that, and when we model out a perfect type of scenario, then we're not going to build in the types of checks and balances to make sure that, when a user does something wrong or they have, for example, a bad credit card, that you're able to capture that and able to model what you want the system to do.

When everything goes right, that's actually a relatively simple thing to model. The complexity comes in when you have to model what happens when one thing or even multiple things *don't* go right. That's where the complexity comes into the system, not only in building out the diagram, but also when it comes to building that into a code base.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+2%3A+Coffee+Ordering+Application/eCommerce+Activity+Diagram)

So, from our start point, the user has a few different branches right from the beginning. So there might be something where they're searching for a product, or they might want to browse categories, or they might want to view previously saved items. So those are the three potential options.

Now, you also could throw in that if you have a number of items just on the home page they could select a product right there, and that would be perfectly fine to add a fourth branch. But for right here, this outlines the core functionality, so that's what I went with for the solution.

From this point, say that we have searched for a product and we have found it. If that's the case, that would take us to a "View product" page. This is where we can view the product. If not, then it should give them the ability to browse categories, and from there they can pick out a product and then be taken to the view product page. Obviously they can also click on "View saved cart items", and it would just take them to the cart page. That's one of the more straightforward approaches.

Also if they want to go straight to the categories, from there they can select the product. Ultimately, no matter what they do, it's going to take them to a view product page.

From this perspective, what we can do is set up the product parameters. So this might be things such as giving them the ability to select different sizes. Since this a coffee ordering service they might be able to say "I want a quantity of 5" or maybe this specific product only has a small or large, and it doesn't have a medium size. So it's being able to set all of that up, which you're going to do in code and then it's going to translate into what they can do in the system. So they're setting up all of the different optional items like quantity and size. And then from there they can add to the cart.

Now this is where we check in and we look at what type of user we're actually working with. So we send it down to a decision point and we check: are they registered? If no, then we're going to send them to a registration page. If they already are registered then we're going to immediately send them to the view cart page.

So let's imagine that they are not registered. They're a brand new user, they come in, they register, they're going to be redirected to the cart page after that.

Hopefully you can see how helpful this could be when you're modeling a system. Essentially what we're doing is, we're taking a user story, we're taking some type of scenario that we want a user to have and the experience we want them to have and we're building out the system. But even though we haven't actually talked about code at all, by being able to look at this type of diagram, you can come in and see the types of pages that you need to create, and even some of the data elements, like product parameters. And then we know that we're going to need to build in user registration. And so you have all of these types of features that, even though we're not explicitly saying, "Go and build this into the system," by analyzing what the experience needs to be, then we can take this, read it, and then go and code it based off of these types of behavior elements.

Now that we're at the View Cart stage, we have the next set of actions. First it checks to see if the cart is OK. It's asking them "Are you sure that you are ready to go? Is everything in the cart correct?" If they say yes, then it takes them down to the Checkout process. If they say no, then it gives them the ability to update the cart. So imagine a scenario where they picked out five elements and they only wanted four or something like that. They can update the cart, and then after it's been updated, we'll still take them to Checkout.

You'll notice I have multiple Checkout options. With these elements, we have some flexibility. These might all be on the same page, or they might all be on separate pages. And so this gives us a little bit of flexibility based off of usually what the UX people have built out. So if you have a set of screens and wireframes this will say that it either needs to be on one page or they may have a step by step process.

So everything there is good, and you'll notice we have no branches from this stage. Now, once everything is in, we check to see if the payment was a success. If yes, then they are redirected to the payment success page and they're done. That's the entire system. If the payment was not a success, for example, if whoever you're using for billing says there was an issue with the credit card, then they're sent to a payment failure page, and it gives them the ability to enter in new information or try again. If they try again, then they're taken back to "Checkout: choose payment type", and if not then we send them to "Update cart." Maybe they remove some items and it takes them through the whole system again.

So this is how you can build out a full activity diagram for an e-commerce system in UML.

##Project Solution: eCommerce Class Diagram

In this guide we're going to walk through the solution for the coffee ordering system's class diagram.

Now, this diagram is even larger than the Twitter project, and it's for a good reason. One of the big items that I wanted to focus on with this is: being able to model what a database looks like for an eCommerce system. One of the very common questions I get from students is how to build out an eCommerce system. And one of the first things I'll usually tell them is to build out the model--to be able to structure the model, because that is going to take you very far down the line in being able to understand the structure of the application. So that is something that as you have gone through this you probably had to spend quite a bit of time in building this out elements such as multiplicity obviously are very important in this. They are in every class diagram. But for this you also have elements surrounding items such as data normalization which is the process of structuring a database in a way that conforms to industry best practices. Now if you're using Lucidchart in screen real estate is valuable then if you come up here you can click on full screen and this gives us a little bit more room. And I'm also going to come down here and give us some zoom. Kind of like we did with the Twitter application.

We're going to pick and choose different classes and focus on those we're not going to talk about every single class mainly because there's going to be duplications throughout the entire set of the explanations so I'm going to focus on what makes this type of class diagram different.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+2%3A+Coffee+Ordering+Application/eCommerce+Class+Diagram.PNG)

I'm going to start off with the taxonomy. This part is, I think, one of the trickier components of this entire system because it utilizes a situation where we don't just have a traditional "one table is related to another." In taxonomy, if you remember back to the instructions, what this represents is a high level abstract kind of class. So this means that we're not going to go and create a set of taxonomies. Instead what we're going to do is we're going to create categories and we're going to create tags, and both of those classes will inherit from the taxonomy class.

This is one of the most important concepts in object oriented programming, which is the ability to find situations where you have one class that can be a parent class and then build out custom versions of that. There are times where this type of class is still a class that you're going to build objects from. So imagine that you had a User class and then you had an admin user that inherited from that user. You might still create user objects and then create a separate set of admin users. But in this scenario this is the way that I'd structure this is to make taxonomy an abstract class. And if you've never heard that term before what that means is it's a class that gives a nice set of foundational rules for how all of the child classes need to behave. It gives items such as an ID, a name, a description, things that are going to be common among all the child classes. But in the program you will never create a taxonomy directly. That's the definition of an abstract class.

Instead, you will create categories. The category class is going to inherit from taxonomy and it's going to add some other elements. So it might say left or right or any of these kinds of items. And those are just thrown out as examples. So this could be quantity, it could be any kinds of things that you feel like a category should represent.

Now tags are different. Both a tag and a category are a type of taxonomy, but they have their own unique qualities. So, here, a tag might just be a different type of weight. So if you wanted to sort your coffee and be able to see all of the items that are over a pound then that's where the tag would come into play. Whereas, with a category, this might give you the type of sorting where you can go and say, "I would like to have only South American coffee blends." Some type of behavior like that.

Now, both, technically at a high level, are a giant category, but they are different enough where they should be split out. And there is one other item I want to point out here before switching. We have a weight and a calculateWeight() that has a different symbol in front of it. Notice with most of these we have plus symbols. What the plus represents is that these are public attributes. What the hash represents is that these are protected.

What that means is that, say that you have another class that inherits from tags. Say that you had some other type of customization where it might be something like 'mobile' tags or something related to that. Then, those inherited classes can call on weight and calculateWeight(), but the objects themselves and any outside systems cannot. These are specifically attributes and operations that are only available to this class and any child classes it may have. And that is how the visibility process works inside of object oriented programming.

Now, going up to Inventory/Product, you may notice that we have the ability to connect products with taxonomies. What that means is that a product can have categories, and it can have tags, and it can do it through the InventoryCategory join table .

You may notice I didn't add the multiplicity elements. And the reason for that is because, one, whenever I have a join table like this, it's always going to be a many-to-many relationship. But the other reason is because this is a little bit more complex. We are connecting a product with a class that will never exist. We'll only have different objects from the inherited classes that will be connected. So I also added this note that says that DB entities are going to implement these many-to-many relationships. And if you remember back to when we walk through the Twitter example, whenever I use a join table I like to use these dotted lines to represent this is not a class it's going to have functionality, it simply is going to have a role where it joins tables together. So we can have a inventory item, and then it could have a category or a tag.

Moving over to the User class, this gets into the discussion of database normalization. Here, you notice that we have a user that has an address, that a user can have many addresses, and that an address can have many users. And if you think that that's weird, think about a real world scenario. Take, for example, Amazon, who pretty much has everybody in the U.S. in their database. Every time that you move someplace else and someone else moves in to your previous address you do not want to say that this one user is the only person that can have that address. That will introduce a very sneaky little bug into your program, because when a user changes their address they're going to get a weird error, because the system is going to say, "I'm sorry. There is already a user with that address." And so that's something that you want to protect against, which is why this is a many-to-many relationship.

Now you might think that city and country are not needed here. And in that regard you may also think that none of these items are needed. There are plenty of times where I've seen developers that structured a database and they loaded up the address, the city, the country, all of those elements inside of the user table. Now that is something I want to highly discourage because you may want a log of everywhere that a user has lived, or, going back to the Amazon example, if you've ever used Amazon you know that it gives you the ability to send to multiple addresses. So I may want to have one address for my home, another address for the office, and other one for a family's residence when I'm sending something to them, and I want to be able to reference those. And that's a reason why I definitely wouldn't put it in the Users table.

Now, why do we need a city class and a country class? Well the reason for this is that it's a part of integrating database normalization. Now, you technically could just tell the user "Type in your city and then type in your country" and let them have at it, and you'd only have this one address class and an associated table. But I personally would prefer to split those out because they're easier to control when all of those elements are in their own type of table. But also it gives us the ability to validate the data. Imagine a scenario where you let users type in their city and country. If they make a typo and they spell their country wrong or they spell their city name wrong, then what could happen is that shipment would go out and it would get returned to you because it had an incorrect address. Whereas, if you keep an entire library of all the countries that are available and then you keep a list of cities--and you may also have seen where the type of process where you can type in your zip code and it will go find your city, state, and country and load all of those in. That is all made possible by splitting these up into their own classes.

So that's something that is definitely important when it comes to structuring your database is to think about how is it important to split up my data. Is it something where all of these elements are simply items that people can type in freehand, or do I need to implement some type of data validation to make sure that it protects against user error and different elements like that.

The last item we're going to talk about is payment. Now if you've ever been to an application where it gave you the option to either type a credit card in or enter your PayPal details, you may have wondered how that would be designed. The way that I would personally do it is that I would create an interface class. You can see that I'm adding in the payment component to say that I'm building a payment interface, and there are going to be a few elements here that are needed. So we need them to type in the payment type, we need to know what the total is, we need to have a reference to the order, and then check to see what the status of the payment is, whether it was declined or if everything went through.

And then we're going to have a credit card class and a PayPal class that both interact with this interface. In other words, these two classes don't inherit from payment. So because credit card is not technically a type of payment, it's a payment source and same with PayPal. It, by itself, isn't a payment. And so what what this type of setup allows us to do is to have much more granular control over how we're setting up the system architecture. Because, for a credit card, this is going to have to go out and communicate with some type of payment gateway. So it's going to have to either interact with Stripe or Authorize.Net. Those are two of the most popular payment gateways out there. And so that means it's going to have its own mini application, in a sense. I's going to have to go connect APIs, it's going to have to wrap up all of the data, it's going to have to have error handling, all of those components right here. You don't want to mix this functionality with what you have with PayPal, because PayPal offers a completely different integration solution. So if these two were merged together and you just tried to create one payment module, and then tried to say, "OK, if a user selects a credit card then go build out this process, or if they select PayPal then go build out this other process," then you're going to end up with a very messy code base.

Instead, the way that I personally would structure it is that I would create classes specifically that implement the payment interface and then they can go and they can manage their own outside connections.

And then lastly, we have this PaymentStatus class that is going to give us the ability to track what the status of the payment is. The reason why I wanted to break this into its own class is because whenever you're talking about any kind of functionality that deals with financial transactions, you need to make sure that you have your entire system covered. You do not want to implement some type of solution where a user could perform a few tasks and get around having a bad credit card, for example.

Imagine a scenario where you didn't build out the right types of checks for when a payment didn't go through. So the card came back declined. But then you didn't build out the entire workflow for saying what steps need to be taken from the user in order to either go and select a different payment method or to simply quit the transaction. If you have holes in your system and you're not capturing this type of payment status correctly, then there might be a situation where someone with a bad credit card would still get their shipment and that is not what you want.

You want to make sure that any type of mission critical elements that really need a high level of security have their own class, so that you can wrap all of the functionality inside of that one class. That's going to make it much easier to understand. Remember, one of the biggest secrets to development is being able to break a system down into as small a set of pieces as possible, so that you can go out and you can focus on one task at a time. Then, in the future, when you want to make changes, you don't have to worry about how each element is intertwined. You can make one change without being worried about effecting another one. When you have a system like that it's called a highly coupled system. It means that if I make a change to this PayPal module it might go and break something in the credit card module. And if you had these both merge together that is a very likely type of scenario. But if you can separate them--and the further you can separate these items out so they do not depend on each other--the better your system is going to be in the long run.
