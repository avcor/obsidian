It refers to multiple piece of works that are working at the same time on different CPU cores. 

`lauch(Dispatchers.Default) {}` this does not guarantee that task will actually execute in parallel. 

`Dispatchers.Default` use a pool of threads. If there are available cores /thread the 2 tasks can execute in parallel. 
