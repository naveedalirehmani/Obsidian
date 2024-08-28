
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


