
```javascript
name: Deploy to AWS EC2

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Check for changes in Node.js server
        id: nodejs_changes
        run: echo "::set-output name=modified::$(git diff --name-only ${{ github.event.before }} ${{ github.sha }} | grep '^nodejs_server/' || true)"
      
      - name: Check for changes in Next.js server
        id: nextjs_changes
        run: echo "::set-output name=modified::$(git diff --name-only ${{ github.event.before }} ${{ github.sha }} | grep '^nextjs_server/' || true)"

      - name: Install dependencies and build Node.js server
        if: steps.nodejs_changes.outputs.modified
        run: |
          cd nodejs_server
          npm install
          npm run build

      - name: Install dependencies and build Next.js server
        if: steps.nextjs_changes.outputs.modified
        run: |
          cd nextjs_server
          npm install
          npm run build

      - name: Transfer files to EC2
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USERNAME }}
          key: ${{ secrets.EC2_PRIVATE_KEY }}
          source: |
            ${{
              steps.nodejs_changes.outputs.modified
                ? 'nodejs_server/'
                : ''
            }} ${
              steps.nextjs_changes.outputs.modified
                ? 'nextjs_server/'
                : ''
            }
          target: |
            ${{
              steps.nodejs_changes.outputs.modified
                ? '/path/to/nodejs_server/'
                : ''
            }} ${
              steps.nextjs_changes.outputs.modified
                ? '/path/to/nextjs_server/'
                : ''
            }

      - name: SSH into EC2 and restart servers
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USERNAME }}
          key: ${{ secrets.EC2_PRIVATE_KEY }}
          script: |
            pm2 restart nodejs_server
            pm2 restart nextjs_server

```

