#Chapter 4 Project 3: Phone Parsing Code Library

##Project Three: Model a Phone Parser Code Library

In Project Three we're going to make a little bit of a change, and design something low-level. Instead of designing high-level user interactions, we're going to design a code library by reverse engineering a Ruby gem that I've built.

This will give you a blueprint of how to design your own gems and code libraries in the future.

The frst type of diagram we're going to implement is a structural diagram: a package diagram, specifically.

### Package Diagram Requirements

* Phone parser
* Country codes

These are going to list out some of the different getters, setters, and methods that are needed in order to allow these to work properly.

A package diagram is very different than a class diagram. It's even more abstract and high-level. It gives more of a sense of how the code is organized and less on how to build it. It's a great for when you're planning a system out, building documentation, or showing how your system operates at a very abstract level.

The second type diagram will be a behavioral diagram. For that, we're going to build a sequence diagram, which focuses on the messages that are sent between between systems, or sent internally. This one is a small code library so it's going to focus on the messages sent inside of the code library itself.

### Sequence Diagram Requirements

* Participants: Parser, Digit length validator, and Country code validator
* Start point: receives data
* End point: returns parsed phone number
* Key messages: Parsing and Validations

This entire code library is focused on validating these phone numbers, parsing them, and then returning cleaned up versions. In the notes for this guide, there is a link to the Ruby gem itself. It comes with examples on how you can run it so that you can test it out and look through it to see all of the other examples and the different features that it contains.


#### Resources

- [Phone Parser Source Code](https://github.com/jordanhudgens/phone_parser)

##Project Solution: Phone Parser Package Diagram

In this lesson, we're going to walk through the package diagram solution for the phone parser project. Now this was a code base that you were given, and the phone parser is going to be one of the more simple UML diagrams that you're going to be doing throughout this entire course.

The reason for that is because it's one of the most high level components. When I'm usually going to build out this type of package diagram it's typically when I'm first thinking about what I'm going to be building.

Now, because of the way that this course is structured, I wanted you to develop a mindset and a mental framework for building out and discovering how you can organize code. You're building this system after looking at the code--which is hopefully a little bit more straightforward than doing it from scratch--but in the future building this type of diagram is going to be the very first thing that you do even before you have entered a single line of code into your editor.

[phone_parser/lib/phone_parser.rb](https://github.com/jordanhudgens/phone_parser/blob/master/lib/phone_parser.rb) :

	require "phone_parser/version"
	require "phone_parser/country_codes"

	module PhoneParser
	  def self.parse(number, country_code: '1')
	    number.delete!("^0-9")
	    digit_length_validator(number)
	    CountryCodes.country_code_validator(number, country_code)
	  end

	  def self.digit_length_validator number
	    number.length < 10 ? (raise PhoneLengthError) : (number)
	  end
	end

	class PhoneLengthError < StandardError
	  def message
	    'Phone numbers need to have at least 10 digits'
	  end
	end


So what we have here is a phone parser. You can see that we have a few modules. We have the phone parser module, and then we bring in the country code module. You don't have to worry about the version; that simply dictates the version of this particular code library.

It's relatively simple what is inside of this. The idea for using this as an example was not to give you an overly complex problem, but instead to give you a really nice case study that you can use for future projects.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+3%3A+Phone+Parsing+Code+Library/Phone+Parser+package+diagram.PNG "Phone Parser Package Diagram")

Notice I added a frame here and I used the shorter version of package--just 'pkg'--so that anyone looking at this will instantly know that it's a package diagram. Inside of it, we just have two modules which, if you look at the codebase, that's all we have there as well. We have PhoneParser, and then we have CountryCodes.

Now I'm drawing this dotted line with an arrow here because a phone parser has a dependency. It depends on the country code. Now that is one of the most important parts of this entire project is being able to see and to visualize where the dependencies in your system are. Because if I were to build out this type of system--if I were to start with this package diagram and then go and start coding--it would instantly tell me that this phone parser cannot live by itself. It is going to have to have a call to this CountryCodes module.

CountryCodes can live by itself. This is simply a helper library. It's not making any calls to PhoneParser. This could just as easily be taken out and applied in a different application. And it does not need PhoneParser. However, if you look at the PhoneParser code library you'll see that it *does* require CountryCodes. And that's part of how it performs the country code part of the validation.

The functionality of this particular Ruby gem is not the most important part of the project. The most important part is being able to see how these are organized. We have two modules, so it makes sense that we'd have two packages, and then be able to add a few items so we can show that there is going to be a number, a country code, and some of the other methods that are inside each one of these items. And also maybe show what type of data structure we're working with.

But here I'm much less concerned about adding a lot of detail. This is still very high level. If I were to build this out and come back and start building out the project afterwards--which is actually what I did--this is the same UML diagram I used before I wrote that entire library. Then I can come and have a really nice idea right away on what type of systems I'm going to have to build in to each one of these modules. And like I mentioned, one of the most critical parts of this entire part of the project is being able to outline the dependencies, because the other part of this that's very important is: imagine that we're going to make some significant changes later on. We're going to say that this phone parser library has to be revamped for adding 10 new features. If I do not have a package diagram right here that shows the different validations, then I could potentially be throwing myself into a situation where I might break this connection on accident. So I might pull out the call to CountryCodes, or I may pull out the CountryCode library entirely or something like that.

Now that may seem implausible, and it's mainly because we only have two modules here, but imagine an application that has 20 different modules or 100 modules. It becomes shockingly easy to pull out one type of module, or one type of class, and not realize that it was a dependency and was being called from another module and so if you have a package diagram then you can when you're later on making changes have a little checklist and say that when I'm making changes to this phone parser library I have to be careful because I know that it relies on country codes. So for me personally one of the most important elements of a package diagram is being able to visualize those dependencies.

##Project Solution: Phone Parser Sequence Diagram

In this lesson we're going to walk through the solution for the sequence diagram in our phone parser project.

If you look at the GitHub page for this project and [go down to usage](https://github.com/jordanhudgens/phone_parser#usage), you'll see that we have a number of different calls we can make. We can call `Parser:parse()`. We also have conditionals, so if a country code is supplied then it will show us what to do then, and it has all kinds of different features that we need to model right here.

You didn't have to do anything besides show how the system could take in data, and how it could send messages back and forth between methods and between modules.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+3%3A+Phone+Parsing+Code+Library/Phone+Parser+sequence+diagram.PNG "Phone Parser Sequence Diagram")

Here, you can see first and foremost who the participants are. This is a relatively small system.

Remember that what these lines present is the role that this particular module or process is going to play inside of the system. So when one of these elements is communicating with the other it's going to have a line. And what this typically represents is that one module or method is sending a message to another module or method. That is one of the key components to understanding how a sequence diagram works is being able to understand how the message sending component of the application is going to operate.

Let's start at the beginning. We're representing a start point by saying that this is when a client or a user is passing in data to `Parser:parse()`. The very first thing that this gets is some type of string data. Now what we're doing is checking to see if it can delete all the symbols except numbers. We remove parentheses, dots, dashes, and we're left with a plain string of numbers. The parse system has the ability to clean out any non-numbers.

Notice how `Parser:parse()` sends a message to itself. Whenever you have a module that's communicating with itself, this is how to visualize it.

After it has performed this process it sends a number length validation message. It sends the string to the `Parser:digit_length_validator()` module. This is simply going to check to see if the number of digits is valid. We'll get an error for anything lower than 10 digits.

The way the messages work is that it has a solid line for when you're sending a message, and then the response is in a dotted line. The reason for that is because we need to be able to visualize that these responses may be different.

After we've gotten the response from `Parser:digit_length_validator()`, then we send a request over to `CountryCodes:country_code_validator()` to check to see if it has a valid country code. It will return an error if the country code is invalid, or give the all clear if it is valid.

The last item, going to our endpoint, is returning a parsed phone number.

That is a basic sequence diagram in UML.
