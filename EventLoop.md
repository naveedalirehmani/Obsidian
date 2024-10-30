
1. **Call Stack Execution (Synchronous Code)**:
    
    - The event loop first executes any synchronous code on the call stack, such as functions and operations directly called in your code.
    - Once the call stack is empty, the event loop moves to asynchronous callbacks.
2. **Next Tick Queue (Node.js Only)**:
    
    - After the call stack clears, the event loop checks for any callbacks in the **next tick queue**, which includes `process.nextTick()` callbacks.
    - **All callbacks in the next tick queue are executed before moving on to the microtask queue**.