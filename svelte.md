
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

### todo list


```ts
<script>
  import { writable } from 'svelte/store';

  let newTodo = '';
  let todos = writable([]);

  function addTodo() {
    if (newTodo.trim() !== '') {
      todos.update(t => [...t, { text: newTodo, completed: false }]);
      newTodo = '';
    }
  }

  function toggleTodo(index) {
    todos.update(t => {
      t[index].completed = !t[index].completed;
      return t;
    });
  }

  function deleteTodo(index) {
    todos.update(t => t.filter((_, i) => i !== index));
  }
</script>

<style>
  .completed {
    text-decoration: line-through;
  }
</style>

<div>
  <h1>To-Do List</h1>
  <input type="text" bind:value={newTodo} placeholder="Enter a new to-do" />
  <button on:click={addTodo}>Add To-Do</button>

  <ul>
    {#each $todos as todo, index}
      <li class:completed={todo.completed}>
        <input type="checkbox" checked={todo.completed} on:change={() => toggleTodo(index)} />
        {todo.text}
        <button on:click={() => deleteTodo(index)}>Delete</button>
      </li>
    {/each}
  </ul>
</div>

```



### svelte.kit

you can create pages like this. 
- `src/routes` is the root route
- `src/routes/about` creates an `/about` route
- `src/routes/blog/[slug]` creates a route with a _parameter_, `slug`, that can be used to load data dynamically when a user requests a page like `/blog/hello-world`

**src/routes/blog/[slug]/+page.svelte**
```ts
<script>
	/** @type {import('./$types').PageData} */
	export let data;
</script>

<h1>{data.title}</h1>
<div>{@html data.content}</div>
```
in the above example data is return from the `+page.ts` or from `+page.server.ts` if it's fetching and returning from an api

**why `+page.server.ts`**
If your `load` function can only run on the server — for example, if it needs to fetch data from a database or you need to access private [environment variables](https://kit.svelte.dev/docs/modules#$env-static-private) like API keys


#### +error
SvelteKit will 'walk up the tree' looking for the closest error boundary — if the file above didn't exist it would try `src/routes/blog/+error.svelte` and then `src/routes/+error.svelte` before rendering the default error page. If _that_ fails (or if the error was thrown from the `load` function of the root `+layout`, which sits 'above' the root `+error`), SvelteKit will bail out and render a static fallback error page, which you can customise by creating a `src/error.html` file.

If the error occurs inside a `load` function in `+layout(.server).js`, the closest error boundary in the tree is an `+error.svelte` file _above_ that layout (not next to it).

```ts
<script>
	import { page } from '$app/stores';
</script>

<h1>{$page.status}: {$page.error.message}</h1>
```

#### +layout.svelte
Just like `+page.svelte` loading data from `+page.js`, your `+layout.svelte` component can get data from a [`load`](https://kit.svelte.dev/docs/load) function in `+layout.js`.

src/routes/settings/+layout.js
```ts
/** @type {import('./$types').LayoutLoad} */
export function load() {	
	return {		
		sections: [			
				{ slug: 'profile', title: 'Profile' },			
				{ slug: 'notifications', title: 'Notifications' }		
			]	
		};
}
```

If a `+layout.js` exports [page options](https://kit.svelte.dev/docs/page-options) — `prerender`, `ssr` and `csr` — they will be used as defaults for child pages.

**src/routes/settings/profile/+page.svelte**
```ts
<script>
	/** @type {import('./$types').PageData} */
	export let data;

	console.log(data.sections); // [{ slug: 'profile', title: 'Profile' }, ...]
</script>
```


### creating a store.

**lib/counter.ts**
```ts
import { writable } from 'svelte/store'

function createCounter(count: number) {
	const { subscribe, set, update } = writable(count)

	function increment() {
		update(count => count + 1)
	}

	function decrement() {
		update(count => count - 1)
	}

	function reset() {
		set(0)
	}

	return { subscribe, increment, decrement, reset }
}

export const counter = createCounter(0)
```
