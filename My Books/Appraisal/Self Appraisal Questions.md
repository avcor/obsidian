
1. Your key achievements during the last year (up to March 2025)
	- Support for android 14 
	- Compatibility with JetPack compose 
	- Offline Support
2. Have you solved any particularly complex mobile-related problems this year? If so, how did you approach and resolve them?
	- Faculty Attendance
	- Remote Config
	- Single File Picker for every feature
	- File Upload component 
	- Installment V-2 (bad code)
3. What new mobile technologies or tools have you learnt or implemented this year? How have they helped you in your role?
	- Jetpack compose 
	- TDD 
	- Dependency Injection 
4. Your Key challenges during the last year and how did you overcome them
	- Migration 
	- Code Mess
5. Your key failures and learning from last year
	- Juggling between the task
	- Consolidated Payments
6. What are your goals for next year, and how are you going to achieve them?
	- Implement Proper Architecture 
	- Code Refactor 
	- Implement Unit test case 
	- Dependency Injection 
	- Modular code 
	- Clean up the mess 



## Questions 

1. Your key achievements during the last year (up to March 2025)
2. Have you solved any particularly complex mobile-related problems this year? If so, how did you approach and resolve them?
3. What new mobile technologies or tools have you learnt or implemented this year? How have they helped you in your role?
4. Your Key challenges during the last year and how did you overcome them
5. Your key failures and learning from last year
6. What are your goals for next year, and how are you going to achieve them?


## Answers 

1. Your key achievements during the last year (up to March 2025) ?
   
	- Support for Android 14 
		- Upgraded Core Technologies 
		  Java -> 8 to  21
		  Gradle Upgrade -> 7.2.0 to 8.7.21
		  Kotlin Update -> 1.4.31 to 2.0.2
		- Removed deprecated ButterKnife, replaced with view bindings (changes impacted 150+ files) and Math-view-Library made it to local .aar for uninterrupted functionality and control over dependencies.
		- Updated Proguard rules to prevent reverse engineering,
		- Made systematic flow for Gradle task, to ensure readability and correct bundling of files for different flavors (i.e Debug, QA, Release). 
	- Compatibility of JetPack compose 
		- While supporting for android 14, I made sure project to be compatible with new technology available. 

2. Have you solved any particularly complex mobile-related problems this year? If so, how did you approach and resolve them?
   
	As I mentioned Above, which are achievements for me are pretty complex and troublesome problems, and with given project It was difficult to make changes and not to break the functioning of existing app. 
	
	- Support for android 14 
		- Approach 
			- I need to fully understand the dependencies and compatibility issues; did quite a research what are the things need to be changed.
			- Estimated a realistic and appropriate completion time and figured out step by step path. Not to mention tackled chain of reaction of upgrades which are mention in question 1 with precedence order.
			- Studied over weekends to research for finding best way possible to do things, so that blocker could be prevented. 
			- Kept tracks of all changes and upgrades. Also, managed other tasks to ensure feature requirement are not affected.  
			- At last, eliminated outdated dependencies, reducing **long-term tech debt**. 
			  
	- Offline Mode in Attendance Taking (Faculty side)
		- Context - Initially believed android did not support offline mode , unlike iOS. I found there some partial implementation of this which is poorly implemented and messy (2000 lines of code in one file).
		- So now how I approached 
			- Re-estimated project deadlines with lead (Mukul) with and without offline support 
			- Went through code base thoroughly, understood the working of already working feature. Interacted with QA for understanding module and different scenarios. Find out what are missing, made a map to follow through, to fill gaps
			- Refactored the unstructured code to make it maintainable, to some extend keeping in mind not break existing functioning and complete feature on time
			- Stuck to my commitment of implementing feature before deadline - I said it, I meant it and did it within decided time. 
	  
3. What new mobile technologies or tools have you learnt or implemented this year? How have they helped you in your role?

	- Jetpack Compose
		- Future-Proofing Our Development - it is future of android development, google is continuously recommending and why I have mention below.
		- There is reduction in boiler code which prevents repetitive code as it is state managed and rely on re-composition. Instead of manually setting up data every time. 
		- It has feature of Hot Reload (BTW which I like in React Native), instead of compiling and rerunning the app.
		- You can make component faster which are independent and easy to reuse, as there is no interaction between XML/Kotlin, which will reduce modification time and development cycle.
		  
	- TDD 
		( During working on Remote Config V2, which enable force update )
		- I know it is a methodology, but the tools I have used such as JUnit, Mockito in android to catch bugs while development, it made sure that the functionality will not break in future modification so I can change code in confidence. 
		- It forced me to think in a modular way, helped me to take my SOLID principle to next level. How could I make it independent of each other while able to test them out and use it in existing flow.
		- Definitely I showed me new way of thinking, improving my code quality. 
		
	- Dagger Hilt 
		- While learning TDD, I came across how to use Dependency Injection, it helped me to understand how and why to decouple components.  
		- It does help me to write better code, even if I did not setup in project right now. How - some of the concept extended my thinking to design more scale able and easy to use maintain Android Application.  
	
4. Your Key challenges during the last year and how did you overcome them
	
	- The project when I started had legacy library, which I found difficult to work with, because it had the gap of what I am knowing and what is there to use. It took a lot research and hit & try to come on a common ground. I tried my best to get generic solution, but if do not get it made sure I had to work around. 
	  
	- Same reason you can take from above, while fixing the bugs, crashes, and ANR (Screen freeze) from crashlytics it was difficult to find in improper written code. I find it is my responsibility to change what I can without hampering the functioning. I Refactored the code, and cleared code messes. Whenever I checked in a module it was cleaner than before. 
	
	- Whenever the task comes we solely relied on spec. It was difficult to work without a given design and deciding what it should look and coding it, then changing it again consumed a lot of development cycle time. That thing I faced during the development of "Consolidated Payments". I approached the UI Designer asked for some help, which she gladly helped.  From there we got a head start and idea what it should look like. When the task completed we were pretty satisfied with results.
	  Now I first ask for the design and what the task main motto, which gives me clear understanding.  
	  
5. Your key failures and learning from last year
	
	- I remember while working on "Hostel & Transport Selection", I was working on support to Android 14 (partially), both of them were very important task. Payments needs to be released and Support to Android 14 apk, need to submitted to google, else they would remove app from play store. 
	  I was really under pressure from both side juggling between the tasks. I started implementing payments module just with specs and rushing to complete it ASAP. I missed to understand the domain, what really it was, what was the "real" product and its edge cases. I created a lot of bugs during that time. I was in sense of false done and given broken app. When it got reported It felt really bad. 
	  How do it solved it - I get the things together, managed time properly, understood everything and fixed my mistakes & code. I determined to fix, even I have to work extra long hours on weekends. At the end I apologized to whom I caused trouble. At the end went all well with scheduled time. 
	  Learning communication when I felt their is delay, instead of using brute force to just complete, I could have raised concern and updated delay. People might have planned or might changed schedule according to it. 
	
6.  What are your goals for next year, and how are you going to achieve them?

	- Proper Architecture & Refactor - Project does not follow proper architecture for most part of it. Correcting those is my first priority.It will be accomplished by simultaneously working on tasks and cleaning up the messes as I touch those modules. This will include code refactor, decoupling classes and implementing state management. At last it will lead to reduced tech debt.
	- Introducing DI (Dagger Hilt) - I have come across that most places resources are opened on Application level context which leaves opened till app is alive, that's memory hogging. By introduction of this, those resources could be opened and recycled on the basis of life-cycle of particular screen. Preventing any kinds of memory leaks. 
	- Implementing TDD & Unit Test through out the app - Yes I have used in "Remote Config Force Update",  but my goal is it to make code unbreakable. To accomplish this I will start implementing this on new task, and if I get chances to work previous modules, I will try implement there as it will be best opportunity change at that moment. This will help me in development, because the problem I have faced during "Hostel & Transport Selection" could be prevented If would check the functionality on just clicking of one button 
	- Changing old previous code to Jetpack compose - We mobile team has planned to change the UI/UX to something better, we have some ideas in mind. Implemntation will take place when there is less of a requirement. Instead of relying of old ways it will be implemented using Jetpack compose with all above mentioned points. This will ensure the project is future safe, unbreakable, and easy to modify. As I work on some modification of existing module, I will present some ideas if it fits the criteria i will implement. I believe this revamp is intensive work, but at least we can just start ball rolling.