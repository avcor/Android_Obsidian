- `setForeground(createForegroundInfo())` promotes the worker to foreground execution and supplies a notification. 
- Work can be rescheduled, but in-memory state does not survive. 
- Making it foreground, give worker a stronger protection against being killed as compared to background worker. 
```
class DownloadWorker(
    appContext: Context,
    params: WorkerParameters
) : CoroutineWorker(appContext, params) {

    override suspend fun doWork(): Result {
        return try {
            setForeground(createForegroundInfo())

            downloadFile()

            Result.success()
        } catch (e: CancellationException) {
            throw e
        } catch (e: IOException) {
            Result.retry()
        }
    }

    private fun createForegroundInfo(): ForegroundInfo {
        val notification = NotificationCompat.Builder(
            applicationContext,
            DOWNLOAD_CHANNEL_ID
        )
            .setContentTitle("Downloading file")
            .setContentText("Download in progress")
            .setSmallIcon(R.drawable.ic_download)
            .setOngoing(true)
            .build()

        return ForegroundInfo(
            DOWNLOAD_NOTIFICATION_ID,
            notification
        )
    }

    private suspend fun downloadFile() {
        // Perform a cancellable download.
        // Persist progress and support safe resumption.
    }

    companion object {
        private const val DOWNLOAD_CHANNEL_ID = "downloads"
        private const val DOWNLOAD_NOTIFICATION_ID = 1001
    }
}
```

