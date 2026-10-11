Lets assume that execution that was happening inside the process is gone. Work Manager does not preserve the Java/Kotlin stack in another process. Instead it uses persisted state to determine that the work is still pending. 

What are the things it needs to remember 
- Work Id 
- Worker Type 
- State 
- Constraints 
- Retry Info 
- Input / Output data