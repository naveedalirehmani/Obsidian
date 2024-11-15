
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

---
### slots

**ChildComponent.svelte**
```ts

<div>
  <h2>Child Component</h2>
  <slot name="header"></slot>
  <div class="content">
    <slot></slot>
  </div>
  <slot name="footer"></slot>
</div>
```

**ParentComponent**
```ts
<script>
  import ChildComponent from './ChildComponent.svelte';
</script>

<main>
  <h1>Parent Component</h1>
  <ChildComponent>
    <h3 slot="header">Header Content</h3>
    <p>Main Content</p>
    <button slot="footer">Footer Button</button>
  </ChildComponent>
</main>
```

---
### side effects and computed values.

in svelte $: is equivalent to useEffect and useMemo is it's called when a state changes. can be used to called side effect or for component values.
```ts
<script>
  let count = 0;

  // Reactive declaration for computed value
  $: doubled = count * 2;

  function increment() {
    count += 1;
  }
</script>

<p>Count: {count}</p>
<p>Doubled: {doubled}</p>
<button on:click={increment}>Increment</button>

```

---
### global state with writables

```ts
<script>
  import { writable } from 'svelte/store';

  // Create a writable store with an initial value
  const count = writable(0);

  // Function to increment the count
  function increment() {
    count.update(n => n + 1);
  }
</script>

<main>
  <h1>Writable Store Example</h1>
  <p>Count: {$count}</p>
  <button on:click={increment}>Increment</button>
</main>

<style>
  main {
    text-align: center;
    margin-top: 50px;
  }
</style>

```
