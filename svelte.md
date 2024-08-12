
### svelte life cycle functions.
```ts
<script>
  import { onMount, beforeUpdate, afterUpdate, onDestroy } from 'svelte';

  let count = 0;

  onMount(() => {
    console.log('Component has been mounted');
    // called after the component is rendered for first time ( called on mount )
  });

  beforeUpdate(() => {
    console.log('Component is about to update with count:', count);
    // called before a value of state is changed with new value and then the component mounts.
  });

  afterUpdate(() => {
    console.log('Component has been updated with count:', count);
    // called on subsequent rerenders and called after the ui is rendered.
  });

  onDestroy(() => {
    console.log('Component is being destroyed');
    // called before the onmount of the component.
  });

  function increment() {
    count += 1;
  }
</script>

<p>Count: {count}</p>
<button on:click={increment}>Increment</button>

```
