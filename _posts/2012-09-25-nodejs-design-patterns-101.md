---
layout: blog
title: Node JS Design Patterns 101
category: blog
tags: [nodejs]  
summery: "I've helped lot of my friends to getting started with Node. These are the problems they were getting into mostly. <br>Learning how to answer these problems will helps you to use Node JS without getting into much trouble."
image: /images/blog/design-patterns.jpg
---

I've helped lot of my friends to getting started with Node. These are the problems they were getting into mostly. Learning how to answer these problems will helps you to use Node JS without getting into much trouble.

##1. How to write a sequence of logic with Asynchronous IO?

What we want to do is, get a user from a database, change his name and notify him via an email.

	var db = getDb(); //there is no such function - only for demo purpose
	var emailer = getEmailer(); //there is no such function - only for demo purpose

	//get the user and call 'doModifyHisName' after we got the user from the db.
	db.get({user: "arunoda"}, doModifyHisName);

	function doModifyHisName(err, user) {

		if(err) {
			//display error once happened and abort the sequence
			console.error(err);
		} else {

			user.name = "Arunoda Susiripala";

			//save the user and call 'doSendEmail' after saving the user
			user.save(doSendEmail);
		}
	}

	function doSendEmail(err) {

		if(err) {
			console.error(err);
		} else {

			//just call 'afterEmailSent' once it has been sent
			emailer.sendEmail(afterEmailSent);
		}
	}

	function afterEmailSent(err) {

		if(err) {
			console.error(err);
		} else {

			//just display the message after executing the sequence
			console.log("arunoda's name changed and notified");
		}
	}

##2. How to execute few tasks parallelly and notifying after all completed?

We need to send few emails at once and display a message after all of them has been sent. In this case we know number of emails we are sending.

	var emailer = getEmailer(); //there is no such function - only for demo purpose

	emailer.sendEmail("arunoda@gmail.com", "You are awesome!", afterEmailSent);
	emailer.sendEmail("kaml@gmail.com", "You are awesome!", afterEmailSent);
	emailer.sendEmail("ranji@gmail.com", "You are awesome!", afterEmailSent);

	var numOfEmails = 3;
	var cnt = 0;
	function afterEmailSent(err) {

		if(err) {
			console.error(err);
		} else {

			cnt++;
			if(cnt == numOfEmail) {
				console.log("All 3 emails has been sent!")
			}
		}

	}

##3. How to iterate over array with some Asynchronous IO

We've an array of userIds. Now we need to print their names in order. But we cannot use a forEach. let's see why?

	var db = getDb();
	var userIds = [10, 20, 30];

	userIds.forEach(function(userId) {

		db.get({_id: userId}, function(err, user) {

			console.log(user.name);
		});
	});

above code will print the names but it is not in order. We may request the db in order, but the database does not send us users in order. This is the nature of asynchronous IO.

Here is how we write it correctly

	var db = getDb();
	var userIds = [10, 20, 30];

	var currId = 0;

	function printName() {

		//get the userId
		var id = userIds[currId++];

		if(id != undefined) {

			//request the db
			db.get({_id: id}, function(err, user) {

				console.log(user.name);

				//call the function again; but this is not recursive
				printName();
			});

		} else {

			console.log("all the names have been printed!")
		}
	}

	//call the function for the first times
	printName();

##4. Same as 1 but need sending email requires the user object

If you notice the #1 of our list correctly we don't see the `user` object in `doSendEmail` method. But  sometimes (most of the time) we need it. 

We can use nested callbacks to overcome this as shown below. 

	user.get(doModifyUser)
	
	function doModifyUser(err, user) {

		user.name = "Arunoda Susiripala";
		user.save(function(err2) {

			emailer.sendEmail(user.email, "Your name is updated!", afterEmailSent);
		});
	}

	function afterEmailSent() {

	}

You can use the above method but sometimes you'll end up with a [Callback Hell](http://callbackhell.com/).
Here's an alternate way to write this without using nested callbacks.

	user.get(doModifyUser)
	
	function doModifyUser(err, user) {

		user.name = "Arunoda Susiripala";
		user.save(doSendEmail(user));
	}

	//this is called currying
	function doSendEmail(user) {

		return function(err) {

			emailer.sendEmail(user.email, "Your name is updated!", afterEmailSent);
		}
	}

	function afterEmailSent() {

	}


##This is not the end

Here I've do not used any NodeJs module to get things done. I just need to show the concept. There are few modules you can use to write NodeJS with less effort. [Async](https://github.com/caolan/async) and [Step](https://github.com/creationix/step) are the most famous. But you should step away from [Node Fibers](https://github.com/laverdet/node-fibers).

Nothing is perfect, this solutions may have bugs and places for improvement. So please share your thoughts!




