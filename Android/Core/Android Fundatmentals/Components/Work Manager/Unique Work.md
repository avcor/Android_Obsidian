Unique work give logical name to sequence of work. 

```kotlin 
val request = OneTimeWorkRequestBuilder<UploadWorker>()
    .build()

WorkManager.getInstance(context)
    .enqueueUniqueWork(
        "ecg_upload",
        ExistingWorkPolicy.KEEP,
        request
    )
```

*The unique policy means that work enqueued under unique name. It does not mean that same worker class is prevented running from other unique name.*
*Also `KEEP` does not mean never run again. Once work is finished, another work under same name can be created.*

## Existing Work Policy options
- `KEEP` - Duplicate trigger will not create duplicate work 
- `REPLACE` - Cancel the existing unfinished work associated name and enqueue the new request. 
- `APPEND` - New request  is added as the dependent of existing sequence. Previous work needs to complete so that new work can start. If work fails or cancelled, then dependent work can be failed or cancelled. 
- `APPEND_OR_REPLACE` - New work will follow pending work, but will not get blocked by failed or cancelled chain. 