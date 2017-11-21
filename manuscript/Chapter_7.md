#Chapter 7 Project 6: Education Assessment Engine

##Project 6: Model an Education Assessment System

In this project, we are going to model an education assessment engine, which is a system that can manage grades for students. It can handles quizzes, projects, assignments, and many other elements to make sure that students are learning the material properly.

We're going to start with one of the more high level diagrams: the activity diagram.

A quick aside: starting with the high level diagrams is a good idea from a practical perspective, but it is also required by the UML specification. It may seem like an interesting thing for UML to specify, but that's because it is so important. In order to be most effective, you need to understand the system as a whole before you try to design any of the smaller pieces. Additionally, employers may have complex project management systems and may request formal UML designs from you, which will need to meet those strict requirements.

### Activity Diagram Requirements

Quiz taking process (6-10 activities)

Roles:

* Teacher
* System
* Student

Example activities:

* Asking a question
* Generating a question set
* Approving results

With activity diagrams (especially ones that have multiple participants like this one) you want to make sure that you're using swim lanes, and that inside of each of those swim lanes you have  activities that are specific to the participant. Make sure that generating a question set falls in line with what the system is responsible for. Each activity should be modeled within the right particpant's roles.

After you've finished the activity diagram it's time for the class diagram.

We're moving to the implementation modeling so quickly because this project is not overly complex. That makes it a great opportunity to research various other elements, as you'll see once we get to the deployment diagram.

### Class Diagram Requirements

* Student
* Klass
* Grade
* Result
* Teacher
* User
* Quiz
* Question
* Essay
* Multiple Choice
* Answer
* Project
* Practice

In many programming languages, you aren't allowed to use the word "Class", because it is a reserved word. In these situations, common convention is to spell it "Klass", as I've done here.

Also, be sure to nest your classes properly (e.g. the 'Teacher' and 'Student' classes are both 'Users').

Even though this is a smaller class diagram than for some of the other systems we've built, it has some surprising and hidden complexities, specifically around 'question' concept. We may have two types of questions, and they both have the ability to have an answer. We don't want to create two answer classes, so the answer has to have an association to both of those question classes.

There is a specific name for this: polymorphic association. Research polymorphic association and see how it can be modeled inside of a UML class diagram. For good reference, I recommend looking through documentation that is specific to Ruby on Rails. You don't have to be a Rails developer in order to understand them or to implement them, but I love the way that they've implemented polymorphic systems in the Rails framework.

Our third diagram is a state machine diagram.

### State Machine Diagram Requirements

Question answering state management

* Waiting for answer
* Answer chosen
* Answer confirmed
* Submit status

This type of diagram models a very small feature, but it gives us a really clear understanding of how the workflow should proceed. In this case, it defines that a user *must* select an answer, and that they aren't allowed to submit the form until they do so.

Our last diagram is a deployment diagram. For this, you'll need to research what is called a "Continuous Integration" service, or CI. I recommend investigating Travis CI, or Codeship (which is what I use for devCamp).

When I push code to, for example, the devCamp servers, I don't push it directly to the server itself. Instead, I push it to the CI server, which performs a number of tasks. The CI server runs database migrations, code checks and tests, and various other processes. If the new code passes the tests, *then* the CI server will push that code along to the other servers.

### Deployment Diagram Requirements

Nodes:

* Continuous Integration (CI) server
* Staging environment
* Pre-production environment
* Production environment

##Project Solution: Education Assessment Activity Diagram

In this lesson, we're going to walk through the solution for the quick passing process in our educational assessment engine project.


![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Activity+Diagram+%23+1317/image1.png)

Now one of the biggest components I wanted you to focus on here is clearly visualizing how each one of the `participants` act and what each one of their activities are going to be. Remember that in an `activity diagram` you can add `swim lanes` so that it can very clearly show all of the processes that are taking place and the roles of the different participants and how those are applied in the system.

So starting off here on the left hand side the entire process gets kicked off by the `teacher assigning the test and quiz` from that point it goes into the `system`. Notice how we have a `teacher` a `system` and a `student swim lane` and then that generates the individual questions set. So that could be something like being able to go and randomize the quiz questions or anything like that.

I modeled this after how the quiz and exam system works in devcamp so this is taken from a real world scenario. Now after the system has done that it gets sent over to the student where they can `confirm` which essentially means that they're saying they're ready to start the process now. From there it goes into this `branch`.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Activity+Diagram+%23+1317/image2.png)

And if you remember from some of our previous solutions this branch is simply here to organize and to visualize the process so that we don't have all kinds of different associations going into a activity by itself. So once the confirmation process happens then it goes down. And it asks the `question` the system asks the question and then it's the student's job to `answer` that.

Now if it was the last question then it's going to continue down and it's going to generate the results if not. So if there are 10 questions and they're on say number five then it simply circles back. And so what we have right here is a loop that is completely based on how many questions that have been answered versus how many are in that specific exam or quiz. And so we'll just keep on going through this loop until it is the last question. Once that's done the system takes in the `results` it generates all of the different scores and then sends it over to the `teacher`. And once the `teacher` gets it they simply approve those results and then the system `stores` them.

So it's a pretty basic kind of test taking process. One of the biggest things that I want you to really focus on here is the ability to visualize the roles of each one of the participants and it's one of the reasons why I really like using swim lanes when I'm dealing with multiple individuals clients user types or anything like that. And I really like putting together this specific type of activity diagram because I think it is a pretty common sense kind of process. This is something that as a student you probably have dealt with in some form or another you've probably had some type of online test taking or quiz taking kind of experience. And so what this does is it can help you understand all of the things that are happening behind the scenes.

Obviously this is meant for an `educational assessment engines` such as a learning management system like devcamp. But this type of process is very common in many different applications where you have one type of user say an `admin` and then they start a workflow the system interacts with a another type of user. It goes back and forth until it gets sent back to the `admin`. That's a common process in many different types of applications. So that's a good one to learn how to model.


##Project Solution: Education Assessment Class Diagram

Next on our list of solutions is our class diagram.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Class+Diagram+%23+1318/image1.png)

Now, this diagram is really not as complex as some of the other ones we've done in this course so far mainly because I wanted you to focus on one very specific topic and that is a `polymorphic Association`. Now that may sound like a really scary word and that's part of the reason why in the requirements video I instructed you to go and research what `polymorphic associations` are. So that you can learn how to integrate them here in the system. So that's really what we're going to focus on before we get to that. I want to show and point out a couple key components on the solution that we have here and also that you have access to in the solution file. And that is how we can represent some of these associations in a little bit of a different way. And so I'm using this as a case study. I am not saying that you needed to build the solution exactly like this. One goal with this course is not only to teach you how to build UML diagrams to solve problems it's also to help you recognize all of the different kinds of UML diagrams and elements that you may see in your day to day jobs.

So here because this guide is all about `associations`. I wanted to point out a few ways that those could be visualized. Right here we have a very basic one. This is just a line connecting one class to another in this case.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Class+Diagram+%23+1318/image2.png)

We have a `quiz` which is connected to a `result` and also notice, I'm not adding any multiplicity here or anything like that. If you did that's fantastic I just didn't want to clutter up the diagram because I wanted this guide to focus completely on how we can visualize `polymorphic kind of associations`. But right here this is a line, now this is perfectly valid UML. You could create a full set of class diagrams that have no arrows. Nothing like that and they only have straight lines that are connecting from one class to another and that is perfectly valid.

Now another way that you could do it is with these type of arrows.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Class+Diagram+%23+1318/image3.png)

Now I highly doubt anyone going through this course will have added that to the solution. And I rarely add these either. These are `composition connectors` so whenever you see one of these big black diamond type of arrows that means that whoever created the diagram is wanting to illustrate that there is a `composition type` of association here and if you're unfamiliar with the concept of composition what it essentially means is that it represents a whole part type of relationship. So in this case we have a `class` which has an association with a `grade` and the `grade` cannot exist without a `class` and then we also have `projects` associated with the `class`. Now this is not so much to say that I wanted this to be in anybody's solution in a real world scenario. I probably would not even add that to my own diagram.

But when ever you're reading someone else's diagram there's a chance you're going to run into these and so I wanted to include them in at least one of these solutions just so you can know what they are and because I know those do look a little bit odd.

Now, know moving all the way here this is now going to start getting us into what this guide is all about which is `polymorphic associations`.

When ever you see an arrow that is completely empty like this

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Class+Diagram+%23+1318/image4.png)

or it's just like this white triangle pointing at an element what that represents is a `generalization type of association` and that is essentially what a `polymorphic association` is. So right here I think we have a good case study. We have a `user` and then it has two types of associations it has a `student` and a `teacher`. Now these both are pointing to the `user` with this type of Arrow because these are generalizations. A `student` is a `user`. A `teacher` is also a `user`. And so they have their own kinds of unique characteristics. A student can have a grade. They can take quizzes whereas a teacher needs to have their degree diploma and different elements like that added.

Now moving all the way over here we have a second type of solution for integrating polymorphism and that is dealing with our questions. So we have a `question` here that has a description a right answer and different elements like that. And then it has a couple of different types of associations and this is literally taken verbatim from the class diagram that is used for devcamp because devcamp in its mid-term and final module has a concept of exam questions and then those questions have multiple types it has a `multiple choice` option and then an `essay` option.

And so these are both classes and they're both types of questions but they have their own unique characteristics a `multiple choice` type question can have a description and then it can have all kinds of different options and I don't have a secondary table showing options but in the devcamp code I do have another table called `Options` that stores the options for each multiple choice question and then that is how multiple choice questions are generated. Now with `essay`s this only has a description and then it does have a right answer but it's not automated. So we have right answers that are placed in the system and they give some guidance for the instructors but there's no way of just saying that a essay question is correct or incorrect so it's a completely different type of setup. This also will change the way that the page loads because if it's an essay question then a large window for them to type code or their full answer is going to appear instead of the multiple choice options. So these are both types of questions but they're stored completely differently because even though they need to represent a question they have very different tasks in how they perform that job.

Lastly one of the most important components on having a `Polymorphic Association` is that both of these classes. Both of these when they get instantiated and they become objects they can be treated the same way. So our student and teacher can't really be treated the same way. So this is a pure `polymorphic` kind of system. It has a number of characteristics of a `polymorphic Association`. However what we have with our questions with `multiple choice` and `essay`. These are a very pure form of the `polymorphic association` and the reason is because of this answer right here. So in order to have a true polymorphic Association what it means is that you can treat each one of these items exactly the same way. So an answer can be its own class its own table and it can interact with multiple choice an essay in an identical manner and that is very important because if we had to build different types of work arounds for `multiple choice` and `essay` then what happens if we start to add additional question types?

All of a sudden this answer class is going to start to get very very messy. But by being able to integrate a polymorphic association it leaves the system in a position where it can be very scalable. We can add as many types of questions as we want and then we can build each of them to be their own polymorphic type of association and then answer can simply work the same way that it always has. And so thats one of the reasons why polymorphic associations are considered a more advanced topic in database design and in application development.

But they are very powerful and so its something that I wanted you to research and learn. And then also learn how to model just like we did right here.


##Project Solution: Education Assessment State Machine Diagram

In this guide, we're going to analyze a potential solution for being able to create a state machine model for answering a question.



![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+State+Machine+Diagram+%23+1319/image1.png)

This is going to be a relatively basic solution because the process that I outlined is pretty straightforward. The goal of this was not to make a very time consuming or complex kind of `state machine`. Instead, it was more to give you a base case so that in the future when you want to reference back and see some of the basic elements and components that a state machine needs you can come and look at this project. So if you remember back to the requirements we simply are looking for the potential states that a student has when they're answering a question. So starting off on the far left here the very first state we have is that the `submit button is disabled` while it's waiting for an answer. So what this means is that if you are handed this type of `state machine diagram` you would know to build in some validations so that the button is disabled until it gets an answer. So in the Start state the button is disabled.

Now if someone clicks on a checkbox and I'm using checkbox as an example it could also be if it's an essay question. If they've entered in a few words or anything like that then what it will do is it will change that status. So the state will change here where it's no longer `disable submit` but now it's watching for it and then it `enables submit` that this is a two way kind of relationship as you can see right here when the check box is set that changes the state.

However if the checkbox is `unset` so if we're in this specific zone right here and where in the state where an answer has been chosen but then the user decides to uncheck the checkbox then it moves back to this state and that is a very critical component in building any kind of state machine diagram. And also just in learning development in general because there are many times where I'll see a project where it looks like it was coated with the attitude that everything was always going to go according to plan.

What I can tell you from my own experience is that that is rarely the case. You need to be able to build in all kinds of redundancies just like we have right here. We need to have this type of two-way relationship where we can switch from one state into another. But then also have the ability to switch back just like we're doing right here and I think this is a pretty good example because if you've ever taken an online quiz or anything like that and you saw how the submit button was disabled until all of the required fields were set. That is essentially what we're modeling right here. Now if an action is taken such as `submitting the button` then it switches to this different state where the answers confirmed and then that is the entire process. So this is a pretty straight forward type of diagram. The most important thing that I want you to take away from it is the ability to change between states and realize that it's not a one way relationship.

You want the ability to say that a user is in state A but then if some actions occur then they can switch from B back and to a. And being able to model that out. That's really one of the top goals of this particular solution.


##Project Solution: Education Assessment Deployment Diagram

In this lesson, we're going to walk through how to design a `deployment engine` for our `educational assessment application`.

![](https://s3-us-west-2.amazonaws.com/devcamp-pictures/Problem+Solving+images/Project+Solution%3A+Education+Assessment+Deployment+Diagram+%23+1320/image1.png)

Now as I mentioned in the requirements of the video the goal of this is for you to learn a few very important dev ops kind of components. The first of which is `continuous integration` and the second is `analyzing a proper workflow` between staging all the way through a production environment.

So this is a relatively straightforward type of deployment diagram we only have four `nodes` and then each of those nodes has just a few components. And the main reason is because I didn't want to add a lot of complexity in regards to designing the diagram I wanted you to focus on learning what some of these components represent. So I'll give you a description of how it works in devcamp.

So whenever I add a new feature or any other developers are working on the system decide to add a new feature to the system they do not just deploy to that. So if I make a few comments and then push up to the master branch then what happens is it goes straight into this `continuous integration server`. I do not skip straight to `production` because of a number of pretty important reasons. If I were to make some changes that would break the server then I want to know about that before users know about that. And so that is one of the most important parts of this `CI system` and that stands for continuous integration and that is that you can look at this almost like your first line of defense. So this is an automated tool.

There are a number of different providers out there `code ship` `Travis CI` there really are countless number of CI providers and they all work in a very similar fashion. I personally prefer `code ship`. I like that they give some nice flexibility with how I can control that server but really you can use any of them. So what happens is as soon as I push to the master branch of devcamp then all of that code gets wrapped up and it gets sent to the `CI server` it gets sent to `code ship` then that's the reason why we have version control is one of the components. And then the service app this is the set of configuration options that I have inside of the `CI server`. So this is going to run all of the `Rspec` tests it's going to run all of the database migrations it's going to perform all of those tasks and that is what we have here with this `artifact` where it's actually going to build the entire application. So assuming that everything works because what happens many times is I'll push something up or another developer will push something up and not realize that maybe we made a dependency version change that would break the entire system. The `CI server` typically will catch those problems. And so assuming that everything passes it builds the system and then it automatically deploys it. So I don't have to deploy the application at all. The `CI servers` in charge of that it deploys to staging.

Now there are a couple nodes here you have `staging` and `pre-production`. Originally, when I built out this diagram I built it modeling it after devcamp and devcamp has a `CI server`, a `staging` and then a `production`. But as I do with all of the different courses that I build. I always take what I've proposed to other developers and other engineers and I show it to them to see if they have any feedback or anything they feel could be a better solution. One of the engineers really recommended that we integrate this `preproduction environment` here and that's a reason why I listed it in the set of requirements not because you need to have it. Like I mentioned I do not have a `pre-production` environment but when I talked with a number of industry engineers they said that they work on applications that have that.

So I wanted to include this right here. There are some very similar types of elements between `staging` and `pre-production` and part of the reason why I personally did not create this type of environment for devcamp but what this typically does is you are going to push to the `CI server` then you're going to go to `staging`. Staging is where you make sure that everything is still on the page and everything is working and that nothing got passed by the `CI server` and you can check it out. Now once that is there this can initiate a copy to pre-production. So if you're working on a very large application and you have a dedicated `QA` team then this is where all of the `QA developers` are going to come in and they're going to test everything out. They're going to run even more tests than what we have in the server. Make sure that everything is working properly.

If it passes all the tests for `staging pre-production` and obviously on the `CI` side then it can finally be deployed to production. And so that is a pretty common type of deployment setup when it comes to modern applications. As I mentioned this `pre-production stage` this is optional but if you are working on a very large application you most likely will see something like this. It's part of the reason why I wanted to include it. But the most important component here is I wanted you to learn what a `CI server` is and how you can use it for not only running tests and those kinds of tools but you can also use that for actually deploying your system so that you personally as a developer are not having to interact with that type of deployment workflow.
