## Process Death
Lets assume that execution that was happening inside the process is gone. Work Manager does not preserve the Java/Kotlin stack in another process. Instead it uses persisted state to determine that the work is still pending. 

What are the things it needs to remember 
- Work Id 
- Worker Type 
- State 
- Constraints 
- Retry Info 
- Input / Output data

## Actions
| Action                    | What it means for WorkManager                                      |
| ------------------------- | ------------------------------------------------------------------ |
| Press Home                | App goes to the background; work can continue                      |
| Swipe app out of Recents  | Does not inherently cancel WorkManager's persistent work           |
| Android kills the process | Current execution stops; eligible work can be rescheduled          |
| User force-stops the app  | Background execution is suppressed until the app is launched again |