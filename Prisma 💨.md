
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
