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

---
### Google Chrome Hacks

* #### Tab Groups: 
If you frequently have many tabs open, the Tab Groups flag can be a lifesaver. Enabling this flag allows you to organize your tabs into groups, which can be collapsed and expanded as needed. To enable this flag, go to `"chrome://flags/#tab-groups"` and select "Enabled" from the dropdown menu.

* #### Scrollable Tab Strip: 
By default, Chrome's tab strip only shows a limited number of tabs, and you have to click on the arrow buttons to see more. However, the Scrollable Tab Strip flag allows you to scroll through all your tabs with a mouse wheel or trackpad gesture. To enable this flag, go to `"chrome://flags/#scrollable-tabstrip"` and select "Enabled" from the dropdown menu.

* #### Reader Mode: 
If you often find yourself reading articles on the web, the Reader Mode flag can make the experience much more pleasant. Enabling this flag removes ads and other distractions, and presents the article in a clean, easy-to-read format. To enable this flag, go to `"chrome://flags/#enable-reader-mode"` and select "Enabled" from the dropdown menu.

* #### Smooth Scrolling:
If you find Chrome's scrolling to be too jarring, the Smooth Scrolling flag can make it more fluid. Enabling this flag applies a smooth animation when you scroll, which can be easier on the eyes. To enable this flag, go to `"chrome://flags/#smooth-scrolling"` and select `"Enabled"` from the dropdown menu.

* #### Experimental QUIC protocol: 
QUIC (Quick UDP Internet Connections) is a protocol that can improve website loading times and make connections more secure. Enabling this flag allows Chrome to use the experimental QUIC protocol instead of the traditional TCP protocol. To enable this flag, go to `"chrome://flags/#enable-quic"` and select `"Enabled"` from the dropdown menu.
