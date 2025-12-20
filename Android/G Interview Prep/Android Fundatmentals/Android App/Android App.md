- Android app is a **linux process** with a **main thread** hosting **android components**
- Activities are just object in those process 

## How application is loaded 
- [[Zygote]] forks a new process 
- App class is loaded (`Application.onCreate`)
- Content Providers init 
- First Activity is create 

## App Startup Types 