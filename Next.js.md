
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
