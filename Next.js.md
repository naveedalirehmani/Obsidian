
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

```tsx
export async function generateStaticParams() {
    const posts = ['dynamic','static']
    return posts.map((post) => ({
      [slug-name]: post,
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

---
### Intercepting routes.

- route intercepting is a very new feature, this allows us to intercept a route and render it's content in a another route. let's consider this scenario, you want to move from route /movie to route /movie/1234 tradition what would happen is that when you click on a list of movies you will be directed to that route and it will be rendered, but before we go to a route we can also intercept it and render it's content in a modal. this is implemented in instagram desktop, when you are watching reels from messages the reel pops up in a modal, upon refreshing the reel opens in a full window. this is also implemented in reddit.
- the specific process to achieve this is challenging to explain in text.

---
### server side vs client side.

**Not to do this**
```tsx
'use client'
 
import ServerComponent from './Server-Component'
 
export default function ClientComponent() {
  const [count, setCount] = useState(0)
  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <ServerComponent />
    </>
  )
}
```

**do this instead!**
```tsx
'use client'
 
import { useState } from 'react'
 
export default function ClientComponent({
  children,
}: {
  children: React.ReactNode
}) {
  const [count, setCount] = useState(0)
  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      {children}
    </>
  )
}
```

---
### client side components

- All components inside the default app router folder are server side rendered, using a special directive 'use client' at the top of the file makes this component client side rendered.
- Any component imported into a client side component is implicitly also render client side.
- so you want to render a server component inside a client side, you should pass it as children, importing it will implicity convert the server component into client component.
- above happens only if SSC is imported into CSC not the other way around! you **CAN** import CSC into SSC.
- if you have a library that uses react hooks, for example a carousal library, you can not directly import it into a SSC. The work around is import it into a completely new component that has 'use client' directive and than import it into SSC.

**NOTE :** CSC are not actually fully render on client side, but are rendered on server side and Javascript is latter hydrated on client side

**When to use client side components?** 
- ==to add interactivity
- ==to use react hooks
- ==to access browser specific APIs

**Tips**
- move client components to the bottom of component tree, so that you don't client side render components that don't need to, example is that when only search bar in navbar has dynamic interactivity, add that that logic in search bar not in navbar.
- props moving for server component to client or vice versa must always be string. things like function cannot be passed!

### server side components

- you don't actually need to pass props for a SSC to SSC because of 2 reasons
	1. any data fetched in one component is cached so calling the api twice will not actually duplicate the request.
	2. if you need to share logic in between, we can you concepts like singleton. 

==__Component Render Sequence for server side components
1. First, all data for a given page is fetched on the server.
2. The server then renders the HTML for the page.
3. The HTML, CSS, and JavaScript for the page are sent to the client.
4. A non-interactive user interface is shown using the generated HTML, and CSS.
5. Finally, React [hydrates](https://react.dev/reference/react-dom/client/hydrateRoot#hydrating-server-rendered-html) the user interface to make it interactive.==

#### Server actions.

In Next.js, we can utilize server components to execute application logic on the server. For instance, if you wish to submit form data to a backend API, traditionally, you'd need to convert a server component into a client component to employ React hooks. However, a new approach allows us to create functions with a `use server` directive placed at the top. These functions, referred to as server actions, are executed on the server. While you can also employ server actions in client components, you'd need to export the server action to its own module for this purpose.

you can use tags on fetch calls to refetch them in next.js or you can revalidate by route path.
   
---
### fonts

You can import fonts from next/font/google and create a font variable like this. you may notice that there are few variables that have a weight property, this is required for non variable fonts you can find the list of all variable fonts here [variable-fonts](https://fonts.google.com/variablefonts) 
```ts
import { Inter, Cedarville_Cursive, Public_Sans } from "next/font/google";

const cursive = Cedarville_Cursive({ subsets: ["latin"], variable: "--cursive", weight:["400"] });
const sans = Public_Sans({ subsets: ["latin"], variable: "--sans", display:'swap' });
```

then define it on the body like to to make this changes apply, also you can do this on each layout level
```tsx
<body className={cn(cursive.className)}>
```

**Method 2**
you can also add a variable property to the font variable function as I did in first example and then reference this variable in your global css file like this.
```css
p{
	font-family: var("--cursive");
}
```

and define it on body like this.
```tsx
<body className={`${cursive.variable}`}>
```

you can also download local fonts and reference them like this.
```tsx
import localFont from 'next/font/local'

const myFont = localFont({
	src: '../static-fonts/Besley-BoldItalic.ttf', 
	display: 'swap',
}）

export default function LocalFontLayout ({children}){

return (
	‹div className={myFont.className}>
		{children}
	</div>
	)
}
```


---

### Server Component Caching. ( app router )

Next.js extends the default fetch api and add extra features on top of it. By default all network requests made are cached and all subsequent requests are returned from cached store ( you can find this in the `.next/cache` folder ).

if you pass `cache: "no-store"` if will not cache the fetch request & refetch on all subsequent requests.

if there are 2 api calls and 1 is default and 1 is `no-store` it will cache first & not cache second on and only if the first request is above the second network call in the code, if the first request with default cache before is placed below the second network request that has `cache: "no-store"` the first request will also not be cached.
but if you have a route segment configurations ( explained below ) this behaviour is not observed.

##### Opting Out Of Caching

1. For individual data fetches, you can opt out of caching by setting the cache option to no-store
2. Once you specify the no-store option for a fetch request, subsequent fetch requests will also not be cached
3. By default, Next.js will cache fetch requests that occur before any dynamic functions (cookies), headers), searchParams) are used and will not cache requests found after dynamic functions

you can also do 
```tsx
export const fetchCache = "default-cache";
```

#### Revalidation
You can also set a expiry on the cache data. pass below option to fetch request.
```tsx
{
	next: {
		revalidate : 10
	}
}
```

### Next.js Api

#### Request.

**Search Params**
```javascript
// Given a request to /home, pathname is /home
request.nextUrl.pathname
// Given a request to /home?name=lee, searchParams is { 'name': 'lee' }
request.nextUrl.searchParams
```

**getting cookies**
```javascript
//access
const accessToken = request.cookies.get("access_token_flower_box")?.value;

//deleting
request.cookies.delete('experiments')

//has
request.cookies.has('experiments')

//clear all
request.cookies.clear()
```

**getting headers**
```javascript
let ip = request.headers.get('X-Forwarded-For')
```

**redirecting**
```javascript
import { redirect } from 'next/navigation'
 
export async function GET(request: Request) {
  redirect('https://nextjs.org/')
}
```

**slugs**
```typescript
//app/items/[slug]/route.ts
export async function GET(
  request: Request,
  { params }: { params: { slug: string } }
) {
  const slug = params.slug // 'a', 'b', or 'c'
}
```

#### Response.

```javascript
import { NextResponse } from 'next/server'
 
export async function GET(request: Request) {
  return NextResponse.json({ error: 'Internal Server Error' }, { status: 500 })
}
```

---

# Next folder structure.

Folder Structure:

```plaintext
├── src/                     # Main source code for the application
│   ├── components/          # Reusable UI components
│   │   ├── ui/              # Basic UI components like buttons, inputs, etc.
│   │   └── layout/          # Components that dictate major page structure
│   │       ├── Header.js
│   │       ├── Footer.js
│   │       └── ...
│   │
│   ├── pages/               # Pages directory for Next.js routing
│   │   ├── api/             # API routes
│   │   │   └── ...
│   │   ├── _app.js          # Custom App component
│   │   ├── index.js         # Homepage
│   │   └── ...
│   │
│   ├── hooks/               # Custom React hooks
│   │   └── useCustomHook.js
│   │
│   ├── utils/               # Utility functions and helpers
│   │   └── ...
│   │
│   ├── styles/              # Global styles and CSS modules
│   │   ├── globals.css
│   │   └── ...
│   │
│   ├── services/            # Services for external API calls
│   │   └── api.js
|   |   └── userService.ts
│   │
│   └── lib/                 # Library code and third-party integrations
│       └── ...
│
├── styles/                  # (Optional) Global styles, if not using CSS-in-JS
│   └── ...
│
├── .env.local               # Local environment variables
├── .env.production          # Production environment variables
├── next.config.js           # Next.js configuration file
├── postcss.config.js        # PostCSS configuration
├── tailwind.config.js       # Tailwind CSS configuration (if used)
└── package.json>)
```

### Axios

```tsx
// src/services/api.ts
import axios, { AxiosInstance } from 'axios';

const axiosInstance: AxiosInstance = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

axiosInstance.interceptors.request.use((config) => {
  // Add auth token or other headers here
  return config;
});

axiosInstance.interceptors.response.use(
  (response) => response,
  (error) => Promise.reject(error)
);

export default axiosInstance;

```

### User api's

```ts
// src/services/userService.ts
import axios from './api'; // Adjust the path as necessary
import { User, UserUpdateData, AuthCredentials } from '../types/user';

class UserService {
  // Fetch user data by ID
  static async getUserById(userId: number): Promise<User> {
    const response = await axios.get<User>(`/users/${userId}`);
    return response.data;
  }

  // Update user information
  static async updateUser(userId: number, updateData: UserUpdateData): Promise<User> {
    const response = await axios.put<User>(`/users/${userId}`, updateData);
    return response.data;
  }

  // Authenticate user and return user data
  static async authenticate(credentials: AuthCredentials): Promise<User> {
    const response = await axios.post<User>('/auth/login', credentials);
    return response.data;
  }

  // Add more user-related methods as needed, such as registration, password changes, etc.
}

export default UserService;

```

### Types

```ts
// types/user.ts
export interface User {
  id: number;
  name: string;
  email: string;
  // Additional user fields
}

export interface UserUpdateData {
  name?: string;
  email?: string;
  // Optional fields for updates
}

// types/apiResponses.ts
export interface
```

# Utils

```ts
// utils/helper.ts
export const formatDate = (dateString) => {
  const date = new Date(dateString);
  return date.toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });
};

```