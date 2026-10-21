- `workManager.cancelWorkById(requestId)` - specific `UUID`. 
- `workManager.cancelUniqueWork("ecg_upload_pipeline")` - unique-work-name 
- `workManager.cancelAllWorkByTag("ecg_upload")` -  particular tag

*Cancelling target request will propagate cancellation to dependent work*

## Gotcha 

Q What will happen when cancellation exception is not caught inside the worker of Work Manager ?
- There are 2 scenarios that android kills the work manager.
	1. If constraints are no longer met, but the app process is still alive
		- In this scenario worker has requested to stop, but `CacellationException()` is swallowed. Your code may execute it further until another check point or suspension point. Work Manger will ignore the `Result.success()` or whatever result. 
	2. Android kills the entire process 
		- Coroutines stops executing because it process no longer exist. 
		- It is not guaranteed that your code will execute further 
- Apart for these scenarios there are changes that you code will not behave as you expected. 
	- Results are ignored, the outcome would not change anything. 
	- Cancellation is caught, but worker is not stopped yet. Block returns failure. Work Manager will treat  it as failure even though exception represented the cancellation of operation. 
```
override suspend fun doWork(): Result {
    return try {
        syncMedicalRecords()
        Result.success()
    } catch (e: CancellationException) {
	    Result.failure() // ❌ Wrong
        throw e // ✅ Preserve cancellation
    } catch (e: IOException) {
        Result.retry()
    } catch (e: Exception) {
        Result.failure()
    }
}
```