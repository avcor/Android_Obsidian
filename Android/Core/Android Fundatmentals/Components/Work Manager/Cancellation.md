- `workManager.cancelWorkById(requestId)` - specific `UUID`. 
- `workManager.cancelUniqueWork("ecg_upload_pipeline")` - unique-work-name 
- `workManager.cancelAllWorkByTag("ecg_upload")` -  particular tag

*Cancelling target request will propagate cancellation to dependent work*