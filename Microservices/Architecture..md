
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

