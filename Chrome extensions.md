
# event flow.

#### If you want to communicate between different parts of the extension:

1. **Background Script** → **Content Script**
2. **Content Script** → **Popup**
3. **Popup** → **Content Script**


---

# Chrome Object. 

### **1. What is the `chrome` Object?**

The `chrome` object is the interface through which you can access Chrome’s extension-specific APIs. This object allows you to interact with various browser features and perform tasks like:

- Opening new tabs or windows.
- Listening to web requests and altering them.
- Accessing storage for saving settings.
- Managing alarms and timers.
