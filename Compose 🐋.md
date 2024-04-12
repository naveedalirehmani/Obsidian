
**postgresql server**
``` yml
version: '3.8'

services:
	postgres:
	image: postgres:latest
	container_name: pg_container
	ports:
		- "5432:5432"
	env_file:
		- .env
	volumes:
		- pgdata:/var/lib/postgresql/data
	restart: unless-stopped

volumes:
pgdata:
```

