Worker defines what needs to be executed (logic)

Results 
- `Result.success()`
- `Result.failure()`
- `Result.retry()`

Policies 
- `BackoffPolicy.LINEAR`
- `BackoffPolicy.EXPONENTIAL` Default
*Backoff policies may reduce retry frequency over time, but it does not guarantee synchronised retries. At backend it can create **thunder-herd** problem. Therefore we need to introduce some jitters in retry policy. For backend we can introduce rate-limiting and & **load shedding** as measure of protection.*
