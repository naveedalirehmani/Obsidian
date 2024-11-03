
## Monolithic applications
Monolithic applications are applications that have all there routing, middle-wares, business logic and database management in one large application to implement **all** features of our application

## Microservices applications
Microservices application are applications that have all there routing, middle-wares, business logic and database management in one multiple applications to implement **one** features of our application.  

### Data management between services.
Data management between services is really challenging. We can tackle this problem in 2 approaches. We can either create synchronous communication between services or asynchronous communication.

#### Synchronous communication.  
in synchronous communication we make direct request between services ( maybe API requests ). There are downsides to this.  

1. By doing so we create dependencies between services, if a service goes down dependent services also goes down. 
2. A request is as fast as the slowest request.
3. Causes web of request, because we might request a service for data but it might internally call two other services for the same request.
4. If an inter service request fails, the overall request fails.
#### Asynchronous communication.
In asynchronous communication we can achieve the same using an event bus, where we emit and catch events between services for communication.

But this basically causes the same problems as mentioned above.

One thing we can do is introduce a different database for the services that need to request other service and populate its database with the necessary data so this service does not has to call other services for query requests at all. With this approach we can also introduce event bus and emit events so that we can populate the database of this services FROM other services. Each time new data comes in.


---

## Authentication Strategies with Microservices
Authentication can be complicated on its own, but when you bring microservices into the picture, it becomes even more challenging. There’s no single "right" way to handle authentication in microservices—it depends on the app’s architecture. Factors like whether you’re using client-side or server-side rendering, and whether you store data in cookies or local storage, all come into play.

Here's a strategy that can be used to handle authentication effectively in a microservices setup.

### Three main issues we need to address:

1. **Preferred authentication strategy**
   The recommended approach is using **http-only cookies** for managing client sessions, paired with **JWT (JSON Web Tokens)** for authentication. 

2. **Who validates the token?**
   We’ll create a **shared library** for validating JWTs. Each microservice will use this library to validate tokens, avoiding the need to forward requests to the **auth** service each time. This has two benefits:
   - No need for inter-service dependencies where every service has to ask the auth service to validate tokens.
   - Each service will be able to handle token validation on its own, without duplicating code in each service.
