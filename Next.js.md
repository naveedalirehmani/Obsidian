  
### Major change

- By default all pages are server side rendered and to achieve this we can just use fetch no need to export functions like serverSideGenerate just like we did in next 12. now the new things is that all pages are cached. Once a page is loaded it’s results is cached this means that going to the same page again will be like visiting a statically generated page, we can also mimic the behaviour of ISR by passing in revalidate to fetch.
- So the new Moto revolves around caching the pages. so concepts like ISR,SSG,SSR are completely different in next 13
- Every page is server side render, unless it is cached, which happens if we use Link in-stead of a or if we visit a page.
- If we pass cache : “no-cache” to fetch this pages will always be server side rendered.
- Pass revalidate to fetch and the page revalidates after a mentioned time period so we achieve behaviour of ISG.
- new default pages such as `page.tsx`, `loading.tsx`, `error.tsx`, `layout.tsx`.
- component streaming in chunks with `loading.tsx` and react __Suspense.__

---
### Why use next/link

- Will prefetch the component for us and for client side caching.
- Client side navigation.
- Soft navigation. Only works for prefetched routes, or if routes don’t have dynamic params.
- Can use href=‘/about#section-id-here’, here we can use # to goto a specific part of the page by giving the same id as #saction-id-here
- Can use replace to delete browser routing history
```tsx
href={{
	pathname: `${
		shop ? item?.href(shop?.toString()!) : item?.href
	}`,
	query: {
		parents: label,
	},
}}
```

---
### Groups

- We can create folder like this `(folder-name)` to group segments. This will not affect the url route for segments. 
- This is just for grouping.
- You can also create multiple root layouts for application partitioning, read more here [Creating multiple root layouts](https://nextjs.org/docs/app/building-your-application/routing/route-groups#creating-multiple-root-layouts)

---
### Layouts

- You can create root level layouts by adding a layout.tsx to app folder, or also for specific segment by adding layout.tsx to each segment
- Remember that layouts are nested, this means that if there’s a root level layout and also a layout in segment. Layout in segment will have root level layout as its layout.
- Can also give layouts to route groups

---
### Template

- Templates are also layouts, but they create new instance for each page. This means that new template instance is create for each page. Can be use full if we want to add render in and render out animation to pages.

---
### Dynamic routes

- Create a folder like this in a segment [folder-name] and the page.tsx of this [folder-name] folder will render on dynamic routes
- […folder-name] will catch all dynamic routes, like /about/id1/id2/id3
- [[…folder-name] ] will catch all dynamic routes, including the leaf 🍁 (page.tsx)

---
### GenerateStaticParams (ONLY-PAGES)

- Export this function from a dynamic route’s page.tsx to pre-render the dynamic routes returned for this method. Because next will know in advance what dynamic routes are going to be called.

```
export async function generateStaticParams() {
    const posts = ['dynamic','static']
    return posts.map((post) => ({
      dashboardId: post,
    }))

}
 ``` 

---
### loading.tsx

- Loading files are used to render a loading component before a component mounts.
- In next.js before a component is mounted on screen it is render on server and then served to client, and then hydration kicks in. So rendering the page on server and then serving it takes time. During this period the loading.tsx file will be rendered.
- If a segment as loading.tsx file, all dynamic routes in that segment will also automatically use this loading.tsx file
- We can also use loading.tsx with react suspense. For example if there are 10 components in a page. next.js does not has to only render the page on the server but also all the components in the pages which might take a while wrapping them in suspense means that this components are streamed. Streamed mean that components are rendered one by one in order and sent to client one by one in chunks where each component is a chunk. For this just wrap for component in a react suspence tag and add a loading component to fallback of suspense.

---
### error.tsx

- With each segment we can add a file called error.tsx which is a fallback if an error occurs in the dynamic route of page.tsx of segment. This will not catch errors in layouts or template. For this add a error.tsx in the parent of segment.
- In app we can add global-error.tsx for global error catching. 
- error.tsx is nested this means that if there is no error.tsx in a segment parent segment will catch the error. But it is better to add error.tsx with each segment.
- We can also use this as fallback component to a react suspense, so that is a component throws error we can catch it.
- error.tsx will receive 2 props error and reset. Error is message and reset if a method that can be called to try and reloading the component that throws error.

---
### Server side rendering.

- By default all pages are static site generate, unless they are dynamic pages of course. If we pass cache : ‘no-store’ to fetch it will fetch on each render. Converting the page into server side render instead of static.
- ==If we don’t use fetch we can export some variables for a component to change the behaviour of the page. Some variables are dynamic = ‘auto’, dynamicParams = true, fetchCache = ‘auto’, revalidate = 0;==

---
### Parallel Routes.

- With parallel routes as the name suggests we can render 2 or more routes in a layout like this.
```tsx
export default function Layout(props: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
}) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  )
}  
```
- create a `@team` and `@analytics` folder in a segment for this, each of these folders will have a `page.tsx` that is the main page.
