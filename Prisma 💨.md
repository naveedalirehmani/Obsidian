
save prisma
```
npm install prisma --save-dev
```

initially a database provider
```
npx prisma init --datasource-provider sqlite
```

only create migration
```
npx prisma migrate dev --create-only --name updated-sessions-table
```

run the created migration
```
npx prisma migrate dev
```

run this to update prisma client after a migration
```
npx prisma generate
```


Prisma connects lets to create a post and than connect it to a user directly
```
const newPost = await prisma.post.create({ 
	data: { 
		title: 'New Post Title', 
		content: 'This is the content of the post.', 
		// Connect the post to an existing user by ID 
		author: { 
			connect: { 
				id: userId 
				}, 
			}, 
		}, 
});
		
```
