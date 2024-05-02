![[diagram-export-13-04-2024-21_08_10.png]]


---
### Scalable Backend Systems Explained

When you want to build a scalable backend system, there are two main approaches to consider:

#### 1. Horizontal Scaling

This means adding more servers to handle increased load. Here are the steps and challenges involved:

- **Load Balancer Setup**: A load balancer is required to distribute incoming requests across multiple servers.
- **Database Load**: Multiple servers may increase the load on the database as they all connect to it simultaneously.
- **State Management**: Managing state across servers is complex. This means you can't easily use session-based technologies that rely on a single server's memory.

**Example**: Imagine a system where requests come in to process transactions (like buying a course). Each server needs to handle the request, process payment, give access, and send an email. If one server handles everything, email delays could slow down the response.

#### 2. Vertical Scaling

This approach involves boosting the resources (like CPU and RAM) of a single server. Here's how it can work:

- **Resource Increase**: You enhance the server's capabilities to handle more tasks simultaneously.
- **Job System Implementation**: Divide tasks into 'critical' (must happen immediately) and 'non-critical' (can be delayed) to optimize processing.

**Example**: A user buys a course:

- _Critical Tasks_: Charge the user and give course access.
- _Non-Critical Task_: Sending an email notification.

Instead of making the user wait for the email to be sent (which takes time), you could:

- **Use a Secondary System**: Send the task of emailing to another server using a job queue system like AWS SQS/ Aevin. This server processes these tasks separately, ensuring the main server responds quickly to the user.

**Additional Considerations**:

- **Rate Limits**: If using a service like AWS SNS which has a cap on notifications (e.g., 400 per minute), set limits (like 300 per minute) to prevent service bans.

### Real-Life Test Case

Let’s apply this to a real-life situation in a learning platform backend:

- **Backend Setup**: Two servers are used. Server A handles user requests for course purchases. Server B handles email notifications.
- **User Buys a Course**:
    - **Server A**:
        - Receives the request.
        - Charges the user.
        - Grants access to the course.
        - Sends a job to AWS SQS to notify the user via email.
        - Responds to the user immediately after granting access, not waiting for the email to be sent.
    - **Server B**:
        - Continuously checks AWS SQS for new jobs.
        - Processes email notifications independently from Server A's operations.
        - Adheres to rate limits to avoid penalties from AWS SNS / Aevin.

This system ensures that critical tasks affecting user experience are prioritized and completed swiftly, while less critical tasks are offloaded to another server, enhancing overall efficiency and scalability.

### Monitoring
Use can use a monitoring services such as Redis insists to monitor the jobs in your queue system.


# Code.

#### Producer Server

```typescript
import express from "express";
import { Queue } from "bullmq";
import { addUserToCourseQuery } from "./utils/course";
import { mockSendEmail } from "./utils/email";

const app = express();
const PORT = process.env.PORT ?? 8000;

const emailQueue = new Queue("email-queue", {
  connection: {
    port: 23898,
  },
});

app.get("/", (req, res) => {
  return res.json({ status: "success", message: "Hello from Express Server" });
});

app.post("/add-user-to-course", async (req, res) => {
  console.log("Adding user to course");
  // Critical
  await addUserToCourseQuery();

  await emailQueue.add(`${Date.now()}`, {
    from: "piyushgarg.dev@gmail.com",
    to: "student@gmail.com",
    subject: "Congrats on enrolling in Twitter Course",
    body: "Dear Student, You have been enrolled to Twitter Clone Course.",
  });

  return res.json({ status: "success", data: { message: "Enrolled Success" } });
});

app.listen(PORT, () => console.log(`Express Server Started on PORT:${PORT}`));
```

#### Consumer server

```javascript
const { Worker } = require('bullmq')

async function mockSendEmail(payload) {
    const { from, to, subject, body } = payload;
    return new Promise((resolve, reject) => {
        console.log(`Sending Email to ${to}....`);
        setTimeout(() => resolve(1), 2 * 1000);
    });
}

const emailWorker = new Worker('email-queue', async (job) => {
    const data = job.data;
    console.log('Job Rec.. ', job.id);

    await mockSendEmail({
        from: data.from,
        to: data.to,
        subject: data.subject,
        body: data.body
    })
}, {
    connection: {
        port: 23898,
    },
    limiter: {
        max: 50,
        duration: 10 * 1000
    }
})

module.exports = emailWorker
```