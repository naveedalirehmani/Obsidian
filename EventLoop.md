
1. **Call Stack Execution (Synchronous Code)**:
    
    - The event loop first executes any synchronous code on the call stack, such as functions and operations directly called in your code.
    - Once the call stack is empty, the event loop moves to asynchronous callbacks.
2. **Next Tick Queue (Node.js Only)**:
    
    - After the call stack clears, the event loop checks for any callbacks in the **next tick queue**, which includes `process.nextTick()` callbacks.
    - **All callbacks in the next tick queue are executed before moving on to the microtask queue**.
3. **Microtask Queue**:
    
    - After processing the next tick queue, the event loop then processes the **microtask queue**.
    - The microtask queue includes promise callbacks (e.g., `.then`, `.catch`, `.finally`) and `queueMicrotask()` callbacks.
    - **All microtasks are processed until the microtask queue is empty**, allowing any newly added microtasks to run before moving on to the next phase.
4. **Task Queue (or Macro Task Queue)**:
    
    - After all synchronous code, next tick queue, and microtasks are complete, the event loop moves to the **task queue**, where it processes one macro task at a time.
    - Macro tasks include `setTimeout`, `setInterval`, `setImmediate` (in Node.js), and I/O callbacks (e.g., file or network operations).
    - Once the task queue processes one task, the event loop checks the next tick queue and the microtask queue again.