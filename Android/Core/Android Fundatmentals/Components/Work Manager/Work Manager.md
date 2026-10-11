Work Manager is Android API for scheduling and executing persistent background work that is expected to eventually run, where you can specify constraints, retries & other execution policy. 

Work that must eventually happen, but does not necessarily control exactly when it happens

Work Manager does not guarantee to be executed once, because your operation can be interrupted & retried. Therefore we need to design work when duplication execution is possible. 

Why delay 
because Android cares for 
- Battery 
- System Resource Usage 
- Constraints 
- Scheduling policy

[[Work Request]]

The app is killed - work manager will die [[Persistence - Process Death]]

[[Worker - Retry]]

