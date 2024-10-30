
1. **Call Stack Execution (Synchronous Code)**:
    
    - The event loop first executes any synchronous code on the call stack, such as functions and operations directly called in your code.
    - Once the call stack is empty, the event loop moves to asynchronous callbacks.