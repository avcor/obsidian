1. Your key achievements during the last year (up to March 2025) ?
- Support for Android 14 
	- Upgraded Core Technologies 
		Java -> 8 to  21
		Gradle Upgrade -> 7.2.0 to 8.7.21
		Kotlin Update -> 1.4.31 to 2.0.2
	- Removed deprecated ButterKnife, replaced with view bindings and Math-view-Library made it to local .aar for uninterrupted functionality and control over dependencies.
	- Updated Proguard rules to prevent reverse engineering
	- Made systematic flow for Gradle task, to ensure readability and correct bundling of files for different flavors (i.e Debug, QA, Release). 
- Compatibility of JetPack compose 
	- While supporting for android 14, I made sure project to be compatible with new technology available. 

2. Have you solved any particularly complex mobile-related problems this year? If so, how did you approach and resolve them?
- Support for android 14 - Approach 
	- I need to fully understand the dependencies and compatibility issues; did quite a research what are the things need to be changed.
	- Estimated a realistic and appropriate completion time and figured out step by step path. Not to mention tackled chain of reaction of upgrades which are mention in question 1 with precedence order.
	- Studied over weekends to research for finding best way possible to do things, so that blocker could be prevented. 
	- Kept tracks of all changes and upgrades. Also, managed other tasks to ensure feature requirement are not affected.  
	- At last, eliminated outdated dependencies, reducing long-term tech debt. 
- Offline Mode in Attendance Taking (Faculty side)
	-  Initially believed android did not support offline mode , unlike iOS. I found there some partial implementation of this which is poorly implemented and messy (2000 lines of code in one file).
	- Approach 
		- Re-estimated project deadlines with lead (Mukul) with and without offline support 
		- Went through code base thoroughly, understood the working of already existing feature. Interacted with QA for understanding module and different scenarios. Find out what are missing, made a map to follow through, to fill gaps
		- Refactored the unstructured code to make it maintainable, to some extend keeping in mind not break existing functioning and complete feature on time.
		- Stuck to my commitment of implementing feature before deadline - I said it, I meant it and did it within decided time. 

3. What new mobile technologies or tools have you learnt or implemented this year? How have they helped you in your role?
   - TDD (While working on Remote Config V2, which enables force update)
     - I applied TDD principles using tools like JUnit and Mockito in android. This helped to catch bugs early in development cycle, gave me confidence during modification and refactor. 
	 - This methodology pushed me to think more in a modular way, help me to apply SOLID principle in better position. It pushed me to create loosely coupled components that could be added into existing flow. 
	 - This showed me new way of thinking, making me more mindful of writing cleaner, more maintainable, and testable code.	   
   -  Dagger Hilt 
     - It helped me to understand the importance of decoupling components, making code more flexible and testable. 
     - Although I have not implemented it in project, yet concept influenced my coding approach.  
   - Jetpack Compose
     - It is future of android development with Google continuously promoting as preferred way of creating UI. Compose significantly reduced boilerplate code by relying on state and composition.
     - With compose, component are faster to build, independent and reusable. Since there is no interaction between XML/Kotlin it reduces complexity of modification.

4. Your Key challenges during the last year and how did you overcome them
   - When I started on the project, I encountered challenges with existing legacy libraries. The gap between my current knowledge and the outdated tech required research and trial-and-error to bridge. Whenever I could not find generic solutions, I applied workarounds to keep development on going without introducing new issues.
   - During bug fixes, resolving crashes and ANR (Application not responding) reported by Crashlytics, the poorly structure and outdated codebase made debugging difficult. I took ownership of code quality whenever I touched a module, I refactored and cleaned up. This helped me understand the code better, as I could clearly see its intent and identify potential changes required in other areas.
   - Whenever a task is assigned, solely relied on the specification. It was challenging to work without a defined design. Coding it and then making changes consumed significant time. I faced during "Consolidated Payments". I approached the designer for help and she gladly helped. This helped to give clear visual direction, making development smother. Now, I make it a point to first request the design and clarify the main objective of the task, which gives me a clear understanding

5. Your key failures and learning from last year
- Context - I remember while working on "Hostel & Transport Selection", I was also handling "support for android 14" partially, both of them were critical and time sensitive. The situation was particularly high pressure because payments needs to be released urgently and Android 14 needs to be submitted to Google Play to avoid app being removed from the store. 
  Failure - I rushed into implementing payment module based on solely on specs, without understanding the domain. I overlooked the products real functionality and its edge cases, which caused numerous bugs. I delivered what I believed to be finished, only to realize later it was incomplete and unstable. When it got reported, I felt genuinely disappointed, knowing it caused trouble for teams. I got things together, managed time properly, understood everything and fixed my mistakes & code. I determined to fix, even I have to work extra long hours on weekends.
  Learning - Instead rushing I could I have communicated about potential delay, allowing team to adjust schedules accordingly. I should have checked functionality before giving it further and should prevented that sense of false done in the big rush. This way of completing work let to extra delays.  

6. What are your goals for next year, and how are you going to achieve them?
* Proper Architecture & Refactor : Current project does not follow proper architecture for most part of it . My intent is to introduce proper architecture by gradually refactoring code while working on ongoing tasks. This will include code refactor, decoupling classes, implementing state to UI. By systematically cleaning up modules as I work on them. I will leave module cleaner, than I last check in.

* Migrating legacy code to Jetpack Compose: Mobile team has planned to revamp the app's UI/UX, and I will be responsible for migrating from traditional XML to Compose with new design. This will require a great amount of time, I will be allocating some extra time to work on these and implement those new features in POC as a side quest (also adding offline mode wherever possible). If I get approval, it will be shipped to the PlayStore as soon as possible. I will keep in mind to interact with UI designers, PMs & other teams.

* Expanding Test Coverage with TDD and Unit Tests: Yes I have previously applied these principles in "Remote Config Force Update", my goal is to broaden test converges across the project. I will implement it into new features, and whenever feasible add test cases into legacy modules as I modify them. For instance, the issue I have faced during "Hostel and transport Selection" could have been prevented with tests.

* Introducing Dependency Injection (Dagger Hilt) for Efficient Resource Management: I have a detailed plan to introduce it into project, as it will be my initial first task from goals.
  Make a side project -> Understand the setup accordance to project + gather info of required library -> Implement basic setup -> Implement changes required ->  Testing. 
  It has a significant impact so I will take it slow and steady, so that it would not halt the functioning.
