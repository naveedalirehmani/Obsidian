
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
