# Retry Pattern

The retry pattern involves retrying a failed operation or request after a
transient failure to increase the likelihood of success

- Many transient failures are self-healing
  - Network issues (e.g., intermittent connectivity)
  - Database deadlocks or timeouts
  - Service rate-limiting due to high load
- Increase reliability
- Reduced failure propagation
- Can combine with Circuit Breaker pattern
- Key concepts
  - Backoff strategy: how system waits between retries
    - Fixed backoff
    - Exponential backoff
    - Jittered backoff: randomness
  - Max retries attempts
  - Idempotency
- Challenges

  - Balancing retry limits
  - Increased latency
  - System overload
  - Error amplification
  - State consistency:

- Tools: Resilience4j, Spring Retry, AWS SDK retries
- Use cases: payment gateways etc

- Example

```java
@Configuration
@EnableRetry
public class PaymentServiceConfiguration {
}

```

```java
import org.springframework.retry.annotation.Retryable;
import org.springframework.retry.annotation.Backoff;
import org.springframework.stereotype.Service;
@Service
public class RetryService {
    @Retryable(
    retryFor = { RuntimeException.class }, // Exceptions to retry on
    maxAttempts = 4, // Maximum retry attempts
    backoff = @Backoff(delay = 2000, multiplier = 2) // Exponential backoff
    )
    public void performTask() {
        System.out.println("Trying to perform task...");
        // Simulate failure
        throw new RuntimeException("Temporary failure");
    }
}
```
