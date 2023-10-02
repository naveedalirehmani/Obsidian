
## Monolithic applications
Monolithic applications are applications that have all there routing, middle-wares, business logic and database management in one large application to implement **all** features of our application

## Microservices applications
Monolithic application are applications that have all there routing, middle-wares, business logic and database management in one large application to implement **one** features of our application.  

### Data management between services.
Data management between services is really challenging. We can tackle this problem in 2 approaches. We can either create synchronous communication between services or asynchronous communication.

#### Synchronous communication.  
in synchronous communication we make direct request between services ( maybe API requests ). There are downsides to this.  

1. By doing so we create dependencies between services, if a service goes down dependent services also goes down. 
2. A request is as fast as the slowest request.
3. Causes web of request, because we might request a service for data but it might internally call two other services for the same request.
4. If an inter service request fails, the overall request fails.
