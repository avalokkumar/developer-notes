### Program that can utilise all the available CPU cores:

```java
public class CPUBoundTask implements Runnable {
    @Override
    public void run() {
        long result = 0;
        for (int i = 0; i < Integer.MAX_VALUE; i++) {
            result += i;
        }
        System.out.println(Thread.currentThread().getName() + " finished with result: " + result);
    }
}

public class CPUBoundApplication {
    public static void main(String[] args) {
        int numThreads = Runtime.getRuntime().availableProcessors();
        ExecutorService executorService = Executors.newFixedThreadPool(numThreads);

        for (int i = 0; i < numThreads; i++) {
            executorService.submit(new CPUBoundTask());
        }

        executorService.shutdown();
    }
}

```

> This program creates a fixed thread pool with the number of threads equal to the available processors, and submits a task that performs a CPU-bound calculation. The program then waits for all tasks to finish before exiting. This will allow all available CPU cores to be utilized to their fullest potential.

---
```python
import multiprocessing

def worker():
    """Worker function that does some CPU-bound work."""
    x = 0
    for i in range(100000000):
        x += i

if __name__ == '__main__':
    # Get the number of available CPU cores
    num_cores = multiprocessing.cpu_count()
    print(f"Running with {num_cores} cores")

    # Start one worker per CPU core
    pool = multiprocessing.Pool(processes=num_cores)
    pool.map(worker, range(num_cores))
    pool.close()
    pool.join()

```

> This program creates a pool of worker processes, with one worker for each CPU core available on the machine. Each worker simply performs a loop that does some CPU-bound work. The pool.map() method is used to distribute the work among the workers, and the pool.close() and pool.join() methods are used to ensure that all the work is completed before the program exits.

> You can adjust the workload by changing the range of the loop in the worker() function. You can also modify the program to perform other types of work, such as I/O-bound work, by using different worker functions.

