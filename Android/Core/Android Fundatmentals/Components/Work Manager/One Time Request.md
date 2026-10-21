## Expedited 
- This is used to tell android that this priority work and should receive priority in scheduling.
- Does not tell ignore every restriction and run immediately, regardless of system state. 
```
val uploadRequest =
    OneTimeWorkRequestBuilder<UploadMessageWorker>()
        .setExpedited(
            OutOfQuotaPolicy.RUN_AS_NON_EXPEDITED_WORK_REQUEST
        )
        .build()

WorkManager.getInstance(context)
    .enqueue(uploadRequest)
```

`RUN_AS_NON_EXPEDITED_WORK_REQUEST` - Falls back to regular work
`DROP_WORK_REQUEST` -  Drops the request
The `setExpedited()` API is for one-time work,
