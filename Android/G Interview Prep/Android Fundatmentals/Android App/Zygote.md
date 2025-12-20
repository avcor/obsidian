- When android OS starts, the init daemon spawns the zygote process
- Zygote is the foundational process that act as parent process for all the application and system processes.

- **Pre-loading** 
  It loads common classes and resources such as Java/Kotlin frameworks and Android libraries in memory heap. 
  Instead of each app loading everything from scratch these child processes inherit the pre-loaded state from zygote, making app startup more faster and memory - efficient.
  It also avoid duplication 
- **Forking**
  When a new app launches zygote fork itself (create a child process)