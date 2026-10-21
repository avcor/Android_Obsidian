```
WorkManager.getInstance(context)
    .enqueueUniquePeriodicWork(
        "medical_record_sync",
        ExistingPeriodicWorkPolicy.KEEP, // mandatory
        syncRequest
    )
```

*minimum 15 min limitation* 

| Policy                 |                                                                                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------- |
| `KEEP`                 | Keep the existing work; ignore the new request.                                                   |
| `UPDATE`               | Update the existing periodic work's specification without unnecessarily cancelling an active run. |
| `CANCEL_AND_REENQUEUE` | Cancel the existing work and enqueue a new request, resetting its scheduling cycle.               |

## Chain 
- You can chain one time request. 
- No periodic node as normal node in work manager chain 