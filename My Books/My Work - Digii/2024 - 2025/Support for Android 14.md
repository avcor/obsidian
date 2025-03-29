
## Tech Impacted 

- Butterknife Removal   
- Gradle Upgrade 
- Kotlin Update 
- Libraries to local - (Such as Math Lib)
- Jetpack Compose
- Proguard Rules  

## Story Line Key Points 

- [[#Why it needed]]
- [[#Tight Deadline]]
- [[#Lot of work]]
- [[#Tasks]] 
- [[#No proper setup]]
- [[#Problems I have faced]]
- [[#How I Solved these problems]] 


### Why it needed 
Every year Google releases the new Android version, with new features and requirements. Previously Digii was supporting till 13 and my task was to take it till 14.     

### Tight Deadline 
Time I was allotted was very less, even I said it was 2 weeks. The task was pretty big and might take more time approximately 1 or 2 week addition. Keeping it in mind that I have to juggle between other tasks. The reason for the task to take so long is that code has not been updated regularly and relying on the legacy modules. 
For example
1. Java - 8 ->  21
2. Gradle - 7.2.0 -> 8.7.21
3. Kotlin 1.4.31 ->  2.0.2
4. Deprecated library -> ButterKnife, Removal of Lib from jCenter (Math Lib and other 2)
5. Compatibility of JetPack Compose 

### Lot of work
First thing first we need to update Gradle to make other things working. This requires the Kotlin upgrade, which require library update of such android core libraries, which require java upgrade, which then requires removal of libraries such as ButterKnife. And unable to find the hosted libraries on JCenter, after update. That is a zest of problems which caused a chain reaction. 
One thing to keep in mind that more than 100's of file have been changed, till date which did not caused any problem till date.

### Tasks
1. Java upgrade
2. Removal of ButterKnife affected file 120 around to proper view binding
3. Gradle upgrade 
4. Make Library to local .arr file and sync with project (Math Lib)
5. Kotlin upgrade 
6. Code upgrade for kotlin
7. Library updates 
8. Implement proper Gradle task to sync with different flavors of app
9. JetPack Compose compatibility
10. Updated pro-guard rule to prevent reverse engineering.

### No proper setup
Project has been not updated regularly. The code was just hanging on the verge of thin thread. Some of things have been upgraded, like Bindings but those were not implemented to whole project, it was just partial implementation. 

### Problems I have faced
It was tight deadline, I have to manage my time and juggle among other priority tasks. It takes a lot of research and development to properly migrate to new stack. It was back and forth of progress, it was causing a lot of problems to migrate, as it was chain of requirement. It was time consuming task to change the code everywhere and make sure it will not impact the app stability. 

### How I Solved these problems  
I have taken some time to understand the depth of the problem and estimated appropriate time completion. I have spend time over weekends to understand the root cause of the problems, so that I could provide the better solution on time. I have managed time with other tasks, so that flow of business is not hampered. 
If I have not estimated time properly or rushed to the problem just for sake of solving it. It may have created a problem for long term and might disrupt the delivery of the new feature to customers. 
I have taken the responsibility of solving the project problem with my full potential, while staying relevant to business requirements too. I understand these type of thing may become blocker in future developments and prevented the rise of sluggishness of the project.