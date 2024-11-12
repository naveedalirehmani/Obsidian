
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

### **2. Important APIs of the `chrome` Object**

Here are some key parts of the `chrome` object:

#### **a. `chrome.runtime`**

This API is used for interacting with the extension's runtime, including managing messages between different parts of the extension (background, content scripts, popup, etc.).

Example:
```ts
// Send a message to the background script
chrome.runtime.sendMessage({ action: 'getData' }, (response) => {
  console.log('Response from background:', response);
});

// Listen for a message in the background script
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  if (message.action === 'getData') {
    sendResponse({ data: 'Here is some data' });
  }
});

```
#### **b. `chrome.tabs`**

This API allows you to manipulate browser tabs, such as opening new tabs or getting information about the current tab.

Example:
```tsx
// Open a new tab with a specific URL
chrome.tabs.create({ url: 'https://www.google.com' });

// Get the active tab's information
chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => {
  console.log('Current tab:', tabs[0]);
});

```

#### **c. `chrome.storage`**

Chrome storage is used to store data persistently, such as user preferences or extension settings.

Example:
```ts
// Store data in Chrome's local storage
chrome.storage.local.set({ theme: 'dark' });

// Retrieve data from Chrome's local storage
chrome.storage.local.get(['theme'], (result) => {
  console.log('Theme:', result.theme);
});

```