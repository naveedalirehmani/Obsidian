
### installation 

```
docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest
```

==once you execute this command it should run a container that exposes 2 ports 
1. 6379 : where the redis server is running
2. 8001 : where the redis-stack is running, you can visualise redis server on this port with browser.

but here we will be using redis-insight that a tool for visualising redis server

if you want to integrate this into `node.js` you can use `ioredis` for this.

### strings.
a single redis string can be a maximum size of 512 mb
##### SET

```
set name naveed
```
to set a string naveed in name variable
```
set name:1 naveed
```
to group strings with versioning.

**SETNX**

```
set msg:1 somtthing nx
```
will only add if msg:1 does not already exists.

 **GET**

```
get msg
``` 
to retrieve a value

##### MGET

```
mget user:1 user:2 msg:1
```
to retrieve multiple values in single operation.

##### MSET

```
mset msg:1 "hello" msg:2 "here"
```
to set multiple values in single transaction

### Integers

```
set count 0
incr count
```
should return 1
```
incrby count 10
```
should return 11

### Expiry 
keys will be delete after a set time period

```
EXPIRE key seconds
```

### List
list is basically an array & it can be used as a stack or a queue depends on the implementation.

```
lpush messages hey
```
similar to unshift in javascript, here messages is the name of the list.
```
rpush message bye
```
similar to push in javascript
```
lpop messages
```
similar to shift 
```
rpop message
```
similar to pop 
```
blpop message 20
```
similar to `lpop` but it's block, this mean that it'll wait for an element to be populated if it doesn't exist, or a specified time period.
```
lrange message 0 -1
```
get all messages


### get by pattren 
```
KEYS msg:*
```
get all message that match the above pattern, here * is placholder for all values.


### sets
unique set of values, similar to arrays in javascript but each unique value may only occur once.

```
sadd ip 1
```
to add a value to set
```
srem ip 3
```
removes 3 member.
```
sismember ip 3
```
should return 0 as removed it above. ( checks for existence of a value in the set )
```
sinter <set-name> <set-2-name>
```
to check for intersections between 2 sets, returns similar values in 2 sets.


#### need to study redis pub sub, this is used to publish and subscribe to events in redis.
( this makes very easy for us to scale web sockets in a micro-services architecture ) 




---

### rate limiting with redis.


**required dev dependencies**
```
npm install typescript ts-node @types/node @types/express @types/ioredis
npx tsc --init
```

```ts
import express, { Request, Response, NextFunction } from 'express';
import Redis from 'ioredis';
import dotenv from 'dotenv';

dotenv.config();

// Initialize Redis client with error handling
const redis = new Redis({
  host: process.env.REDIS_HOST || '127.0.0.1',
  port: parseInt(process.env.REDIS_PORT || '6379', 10),
  retryStrategy: (times) => {
    const delay = Math.min(times * 50, 2000);
    return delay;
  },
});

redis.on('error', (err) => {
  console.error('Redis error:', err);
});

const app = express();
const PORT = process.env.PORT || 3000;
const WINDOW_SIZE_IN_SECONDS = parseInt(process.env.WINDOW_SIZE_IN_SECONDS || '60', 10);
const MAX_WINDOW_REQUEST_COUNT = parseInt(process.env.MAX_WINDOW_REQUEST_COUNT || '10', 10);

interface RateLimiterRequest extends Request {
  ip: string;
}

const rateLimiter = async (req: RateLimiterRequest, res: Response, next: NextFunction) => {
  try {
    const ip = req.ip || req.headers['x-forwarded-for']?.toString() || req.connection.remoteAddress;

    if (!ip) {
      return res.status(400).json({ message: 'Unable to determine IP address' });
    }

    const currentRequestCount = await redis.incr(ip);

    if (currentRequestCount === 1) {
      await redis.expire(ip, WINDOW_SIZE_IN_SECONDS);
    }

    if (currentRequestCount > MAX_WINDOW_REQUEST_COUNT) {
      return res.status(429).json({ message: 'Too many requests, please try again later.' });
    }

    next();
  } catch (error) {
    console.error('Error in rateLimiter middleware:', error);
    return res.status(500).json({ message: 'Internal server error.' });
  }
};

app.get('/ratelimit', rateLimiter, (req: Request, res: Response) => {
  res.send('This is a rate-limited route.');
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

```


