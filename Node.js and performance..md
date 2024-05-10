
performance of the server really matters, as a survey states that load times of more then 3 seconds caused 73% of users to lose interest, if a process that is supposed to be fast but takes time, let say a user is doing a survey and is switch between articles, this process is suppose to be fast response time of more then even as low as 1 second can cause user to lose track of what he wanted to do.

to solve this issue we create load balancing, one of the approaches called RoundRobin is used to achieve load balancing in a node.js is discussed below.

when we start a node process by let say calling node index.js node create a primary process called master and every time we call cluster.fork() here cluster is required from a built in node.js module called cluster, node keeps on creating worker process, this means that we can create multiple processes that each can respond to requests on there on, on linux distributions such as Ubuntu or macOS request are assigned to individual process VIA round robin approach.

Round Robin approach is when lets say we have three processes a master and two workers if both of workers are in processing a request the third request will again be assigned to the first worker and then the 4 request to second worker, this works in a loop. on windows how ever node leaves this process of divided requests between workers to windows it self, so it might use round robin or any other approach. remember only workers accept requests.

one might ask, if this is the case why don’t we create as many workers as we want? well there is a limit to it, our each worker works on a different cpu core, this means that if our cpu has 4 physical cores we should not create more workers as our machine’s cpu might not be able to handle this, I say might not be here because our modern cpus also have logical core not just physical cores, so our node js can use these logical cores also to create more workers.

so to do this task efficiently we use node.js built in module called os, os.cpus() will give the numbers of physical/logical threads combined, now we have to just loop over it and call cluster.fork() in each iteration to create a worker process.

this way we can efficiently achieve a better performance from over server, in simple words we horizontally scaled our server.
this is working but there is a better way of doing this with third party libraries such as pm2, which offers much more easy solutions to such complex problems but remember that pm2 also uses node.js built in cluster module.

### USING PM2

- PM2 list => current status of the server
- pm2 stop 0 =>  this is to stop a single process/worker , 0 is the id of the worker which you can find by typing pm2 list.
- pm2 start server => to start the server with pm2, server is the name of the process. 
- pm2 delete server => server is the name of the process.
- pm2 start server.js -i 2/max => this will execute the server.js, and -i 2 or -i max flag here means that create 2 or maximum number of capable process here.
- pm2 restart server => restart a process or processes if all have server as their name.
- pm2 logs / r => to list the logs on the server or last 200 logs on the server.
- pm2 start server.js -l logs.txt -i max => start max number of workers for server.js file and output logs to logs.txt.
- pm2 show 0 => gives detail information for a specific process.
- pm2 monit => this create a monitor in terminal showing a lot more detail on the status of ever process.
- pm2 reload server => here server is the name of the process and all our processes are called server, reload and restart are very different, restart will restart app processes at once will reload will restart them one by one, so that there is always one process running, this insures that our server has not downtime.


### Package.json & Package.lock.json
  
- instead of creating our own modules we can use third party modules, like we can replace http module that comes with node.js with axios, we keep track of the the modules/packages that our project depends on with package.json file where we can also configure our own project which is also a package that depends on axios, and axios can also depend on another package, so there is a dependency tree, like axios uses follow request for any redirects that our url may require. so when we install axios npm also installs follow-request which will not be listed in our package.json file but in the axios module package.json file. if two third party modules depend on a same package lets say axios and mongoose both use follow-request it will not install twice.

#### MAJOR.MINOR.PATCH
**2.1.3**
- Here 2 is major, changes that completed change the package.
- 1 is a minor changes that adds extra functionality.
- 3 this is for just bug fixes.
- Package.lock.json file
- this file keeps track of extra information such as exact version number of the package we are using and also keeps track of all the package the package depends on, you might have seen ^2.1.3 in package.json file, here ^ means that the package will install with the latest minor version.
- sometimes when installing a package we get high vulneberity error, this means that a security issue was fixed in a latest version of this packages that we have not install, npm audit will check to see if their are any security issue in the current version of the package and npm audit fix will fix it just by installing the newer version where security issue was fixed by the package developers.
- If we have to different server like client and server for a react and node.js file , we would what usually do is use 2 different terminals to manage both servers and their npm commands, what we can also do is create a package.json file in the main folder where both client and server live and manage both servers from their

```json
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1",
"server": "cd server && npm run dev", // first cd to server folder and then run npm run dev
"client": "npm run start --prefix client", // first cd to client folder and then run npm run start
"install-client": "npm install --prefix client", // first cd to client and run npm install
"install-server": "npm install --prefix server", // first cd to server and run npm install
"install": "npm run install-client && npm run install-server" // run both npm run install-client and then run npm run intsall-server.
"watch": "npm run server & npm run client”, // run both commands npm run server && npm run client, here single & means that do not weight for first script to end.
"deploy": "npm run build --prefix client && npm run server", // this does alot runs npm run build in client folder and then runs npm run server which then first will cd into server and run npm run dev.

}
```

- **How to deploy such apps that are mentioned above, Deployment.**
- build the react app and then copy the build folder to node.js server where our build files will live in public folder and then using express middleware app.use(express.static(path.join(_dirname,’public’)) we can server them publicly, so that we don’t have to deploy both server on different plate forms such as node.js on heruko and react on netlify.  to avoid copy pasting build files manualy use **_"build": "BUILD_PATH=../server/public react-scripts build",_**   in react package.json file.