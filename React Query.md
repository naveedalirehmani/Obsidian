
**isError**
returns error status
boolean

**error**
contains error message
string

**isLoading** v5 -> **isInitialLoading**
is fetched data loading
Boolean.

**data**
contains the data
return data

**isFetching**
initially when the page loads for the first time, react query fetches data and caches it, but when you visit a page second time cache data is displayed on the page
this means that on second time isLoading will always be false, also react query will do a background fetch and if the newly fetched data does not matches the
cache data it will update the UI, isFetching indicates that background refetch.
Boolean.

**cacheTime**
cacheTime the time period for which cache data is stored after that cache data is deleted.

**staleTime**
By default every visit to the page will trigger a background refetch just to make sure that we always have latest updated data, we can also stop this behavour
by providing a staleTime period, in this time frame no background refetching will occur. this keeps data fresh.

**refetchOnWindowFocus**
this will refetch data on window focus, such as changing tab and coming back to application tab.

**refetchOnMount**
this by default is set to true, means it will cause background refetching, every time windows is mounted.

**refetchInterval**
this will fetch query in intervals

**refetchIntervalInBackground**
this will fetch query in intervals even if window loses focus

**refetch**
call this function to fetch queries on events, such as fetch onClick.

**enabled**
this will disable query, this means that data will not be fetch even on mount, only on events such as refetch.

**onSuccess, onError**
two callbacks that are called on query error or success receives error object or data in params respectivaly,

**select**
lets you transform data before caching it.

**dynamic queries**
this is not a react query callback or configration, instead of this useQuery(‘name’) you can do this useQuery( [ ‘name’ , id ] ), this
is to fetch specific item by key not every item, by doing this we can receive queryKey in the fetcher function as param, and reactQuery
will maintain a seperat query for seperat id.

**data : friendsData**
this is how you can you alias to data, this will be helpful when using multiple useQueries in same component**initialData**
this is a callback that set initial data so we have something to render before even we receive over response, returned data will be initial data.

**getQueryClient**
correct syntax is queryClient.getQueryData(‘name’) this is to get already cached query data manually by it’s name, here queryClient is 
created by useQueryClient which is imported from library, use case is to set initial data.
e:g queryClient = useQueryClient

**keepPreviousdata**
keepPreviousdata will keep previous query data, for example when working with dynamic queries each item is fetch with it’s respective id
every time we will receive new data, but when id changes data changes and old cached data is deleted this will keep track and save all
previous fetched queries by id, so let’s say it will make our application faster, such as pagination.


---
### Notes.

```tsx
const { mutate: createShop, isLoading: creating } = useCreateShopMutation();
```

```tsx
export const useCreateShopMutation = () => {

const queryClient = useQueryClient();
const router = useRouter();

  
return useMutation(shopClient.create, {
	onSuccess: () => {
		const { permissions } = getAuthCredentials();
		if (hasAccess(adminOnly, permissions)) {
			return router.push(Routes.adminMyShops);
		}
	router.push(Routes.dashboard);
	},
	onSettled: () => {
		queryClient.invalidateQueries(API_ENDPOINTS.SHOPS);
		},
	});
};
```

**crud factory**
```tsx
export function crudFactory<Type, QueryParams extends LanguageParam, InputType>(

endpoint: string

) {

return {

all(params: QueryParams) {

return HttpClient.get<Type[]>(endpoint, params);

},

paginated(params: QueryParams) {

return HttpClient.get<PaginatorInfo<Type>>(endpoint, params);

},

get({ slug, language }: GetParams) {

return HttpClient.get<Type>(`${endpoint}/${slug}`, { language });

},

create(data: InputType) {

return HttpClient.post<Type>(endpoint, data);

},

update({ id, ...input }: Partial<InputType> & { id: string }) {

return HttpClient.put<Type>(`${endpoint}/${id}`, input);

},

delete({ id }: { id: string }) {

return HttpClient.delete<boolean>(`${endpoint}/${id}`);

},

};

}
```

**http client**
```tsx
export class HttpClient {

static async get<T>(url: string, params?: unknown) {

const response = await Axios.get<T>(url, { params });

return response.data;

}

  

static async post<T>(url: string, data: unknown, options?: any) {

const response = await Axios.post<T>(url, data, options);

return response.data;

}
```

