
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
5. **Re-check for Next Tick Queue and Microtasks**:
    
    - After each macro task completes, the event loop again checks for and executes any callbacks in the **next tick queue** and then the **microtask queue** before processing the next task from the task queue.
    - This cycle continues until all tasks, next tick callbacks, and microtasks are exhausted.
6. **Iteration Continues**:
    
    - This process of checking the next tick queue, microtask queue, and task queue continues on each event loop tick, handling tasks as they appear and looping until the event loop has no more work to do.

### Summary Flow of Each Event Loop Iteration:

1. Execute **synchronous code** on the call stack.
2. Execute all callbacks in the **next tick queue** (`process.nextTick`).
3. Execute all callbacks in the **microtask queue** (e.g., `Promise` callbacks, `queueMicrotask`).
4. Execute one **task from the task queue** (e.g., `setTimeout`, `setImmediate`, I/O events).
5. **Re-check the next tick queue** and **microtask queue**.
6. Repeat steps 4–5 until the task queue, next tick queue, and microtask queue are empty.
