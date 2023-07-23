### 12 Factor principles

#### 1. Codebase: 
One codebase tracked in revision control, many deploys. This factor emphasizes the importance of maintaining a single codebase that is tracked in revision control, such as Git. This allows for easy collaboration and versioning of the code, as well as the ability to deploy the same codebase to multiple environments, such as development, staging, and production.

> An example of this is using Git as a revision control system to maintain a single codebase and multiple branches for different environments(dev,staging,production)


#### 2. Dependencies: 
Explicitly declare and isolate dependencies. This factor emphasizes the importance of clearly declaring and isolating dependencies for the application. This can be done using a package manager, such as npm or pip, and by using virtual environments to isolate dependencies for different projects.

> An example of this is using a package manager like npm or pip to manage dependencies, and using virtual environments to isolate dependencies for different projects.

#### 3. Config: 
Store config in the environment. This factor emphasizes the importance of storing configuration information, such as API keys, database credentials, and other sensitive information, in environment variables rather than hard-coding them into the code. This makes it easier to change configuration information without modifying the code and also keeps sensitive information out of the codebase.

> An example of this is using environment variables to store sensitive information like API keys, database credentials, and other configuration.

#### 4. Backing services: 
Treat backing services as attached resources. This factor emphasizes the importance of treating backing services, such as databases, message queues, and caches, as attached resources rather than hard-coded dependencies of the application. This allows the application to be easily moved between different environments, such as development and production, without having to change the code.

> An example of this is using a database as a service like AWS RDS or Heroku Postgres

#### 5. Build, release, run: 
Strictly separate build and run stages. This factor emphasizes the importance of separating the build, release, and run stages of the application. The build stage is responsible for compiling the code and creating a release, the release stage is responsible for packaging the code and configuration, and the run stage is responsible for executing the code.

> An example of this is using a CI/CD tool like Jenkins or CircleCI to automate the build, release, and run stages of the application.

#### 6. Processes: 
Execute the app as one or more stateless processes. This factor emphasizes the importance of running the application as one or more stateless processes. Stateless processes do not maintain any data in memory, which makes it easier to scale and deploy the application.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to run the application as one or more stateless processes.

#### 7. Port binding: 
Export services via port binding. This factor emphasizes the importance of exporting services via port binding. This allows the application to be easily moved between different environments, such as development and production, without having to change the code.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to export services via port binding.

#### 8. Concurrency: 
Scale out via the process model. This factor emphasizes the importance of scaling out the application by running multiple processes in parallel. This allows the application to handle more traffic and provides more redundancy.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to scale out the application by running multiple processes in parallel.

#### 9. Disposability: 
Maximize robustness with fast startup and graceful shutdown. This factor emphasizes the importance of maximizing robustness by ensuring that the application can be started and stopped quickly and gracefully. This allows the application to be easily moved between different environments, such as development and production, without having to change the code.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to maximize robustness by ensuring that the application can be started and stopped quickly and gracefully.

#### 10. Dev/prod parity: 
Keep development, staging, and production as similar as possible. This factor emphasizes the importance of keeping the development, staging, and production environments as similar as possible. This allows for more predictable and consistent behavior across different environments, and makes it easier to move the application between different environments.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to keep development, staging, and production as similar as possible.

#### 11. Logs: 
Treat logs as event streams. This factor emphasizes the importance of treating logs as event streams, which allows for real-time analysis and troubleshooting of the application. It also allows for the logs to be centralized, searched and indexed for later analysis.

> An example of this is using a log aggregation tool like Splunk or ELK to treat logs as event streams.

#### 12. Admin processes: 
Run admin/management tasks as one-off processes. This factor emphasizes the importance of running admin and management tasks as one-off processes. This allows for a clear separation of concerns between the application and the admin tasks, and makes it easier to automate and manage the tasks.

> An example of this is using a container orchestration tool like Kubernetes or Docker Swarm to run admin and management tasks as one-off processes.

---
[More details](https://12factor.net/)
