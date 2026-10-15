## Basics
```kotlin
WorkManager.getInstance(context)
    .beginWith(uploadRequest)
    .then(updateRequest)
    .then(cleanupRequest)
    .enqueue()
```
```
UploadEcgWorker
       |
       v
RETRY or FAILURE
       |
       v
UpdateSessionWorker
       |
       v
CleanupWorker
```

- If upload is retry then work is eligible for another attempt according to scheduling rules. Dependents work waits. 
- If upload is failed, dependent work does not run. Failure will propagates through dependent chain. 
- If upload is cancelled then dependent work is cancelled. 

## Parallel
```kotlin 
WorkManager.getInstance(context)
    .beginUniqueWork(
        "ecg_upload_pipeline",
        ExistingWorkPolicy.KEEP,
        upload
    )
    .then(listOf(updateProfileRequest, updateAnalyticsRequest))
    .enqueue() 
```
```
          Upload
          /    \
         /      \
UpdateProfile  UpdateAnalytics
```

Here whole sequence have same named pipeline, and `KEEP` retains existing sequence. 

Work names are attached to unique-work sequence not individual nodes in chain. If you want to do this then you not design the enqueue strategy around it.