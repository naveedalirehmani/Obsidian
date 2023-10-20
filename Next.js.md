
#### Major change

- By default all pages are server side rendered and to achieve this we can just use fetch no need to export functions like serverSideGenerate just like we did in next 12. now the new things is that all pages are cached. Once a page is loaded it’s results is cached this means that going to the same page again will be like visiting a statically generated page, we can also mimic the behaviour of ISR by passing in revalidate to fetch.
- So the new Moto revolves around caching the pages. so concepts like ISR,SSG,SSR are completely different in next 13
- Every page is server side render, unless it is cached, which happens if we use Link in-stead of a or if we visit a page.
- If we pass cache : “no-cache” to fetch this pages will always be server side rendered.
- Pass revalidate to fetch and the page revalidates after a mentioned time period so we achieve behaviour of ISG.

#### Why use next/link

- Will prefetch the component for us and for client side caching.
- Client side navigation.
- Soft navigation. Only works for prefetched routes, or if routes don’t have dynamic params.
- Can use href=‘/about#section-id-here’, here we can use # to goto a specific part of the page by giving the same id as #saction-id-here
- Can use replace to delete browser routing history

#### Dynamic routes

- Create a folder like this in a segment [folder-name] and the page.tsx of this [folder-name] folder will render on dynamic routes
- […folder-name] will catch all dynamic routes, like /about/id1/id2/id3

#### Groups

- We can create folder like this (folder-name) to group segments. This will not affect the url route for segments. 
- This is just for grouping.

#### Layouts

- You can create root level layouts by adding a layout.tsx to app folder, or also for specific segment by adding layout.tsx to each segment
- Remember that layouts are nested, this means that if there’s a root level layout and also a layout in segment. Layout in segment will have root level layout as its layout.
- Can also give layouts to route groups

#### Template

- Templates are also layouts, but they create new instance for each page. This means that new template instance is create for each page. Can be use full if we want to add render in and render out animation to pages.

#### Dynamic routes

- Create a folder like this in a segment [folder-name] and the page.tsx of this [folder-name] folder will render on dynamic routes
- […folder-name] will catch all dynamic routes, like /about/id1/id2/id3

#### loading.tsx

- Loading files are used to render a loading component before a component mounts.
- In next.js before a component is mounted on screen it is render on server and then served to client, and then hydration kicks in. So rendering the page on server and then serving it takes time. During this period the loading.tsx file will be rendered.
- If a segment as loading.tsx file, all dynamic routes in that segment will also automatically use this loading.tsx file
- We can also use loading.tsx with react suspense. For example if there are 10 components in a page. next.js does not has to only render the page on the server but also all the components in the pages which might take a while wrapping them in suspense means that this components are streamed. Streamed mean that components are rendered one by one in order and sent to client one by one in chunks where each component is a chunk. For this just wrap for component in a react suspence tag and add a loading component to fallback of suspense.
