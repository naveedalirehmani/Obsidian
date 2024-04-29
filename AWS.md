### How to create a very simple aws ubunto instance

1. create a __aws instance.
2. log into this __aws instance__ with your __ssh key__. ( ssh is just secure shell to connecting remote computers. )
3. once logged into __aws instance__ type `sudo apt update` this will find any out dated packages on your __ubunto instance__
4. type `sudo apt upgrade` to upgrade any outdate packages.
5. type `sudo install apache2` to install __apache web server__ ( for listening to incoming http web traffic )
6. type `cd /etc/apache2` this is where you __apache web server__ files are installed.
	1. `cd` into `sites-available` folder and you will find 2 files.
	2. `000-default.conf` for listening to http request.
	3. `default-ssl.conf` for listening to https request.
8. type `cd /var/www/html` this is where you will find __index.html__ what is served by `000-default.conf` on port __80__.
9. type `sudo vi index.html`
10. you can update this file by typing `d100d` to delete 100 lines or as many as you want. press __i__ on keyboard to go into insert mode on vim to update this file. 
11. Once you are done with the necessary changes, press __ESC__ and press __shift+z+z__ to save and exist this file.
12. goto __aws instance__ and open __security groups__ for this instance. update firewall in __inbound rules__ tab to add a new __IPv4 http__ port on port __80__ to open listening to incoming public requests on the web.
13. type in your public ipv4 into browser for this instance and you should see your changes.


```
server {
    listen 80;
    server_name docker.naveedalirehmani.online;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

```

---

## Setting up ec2.
```
sudo apt-get update
```

```
sudo apt install curl 
```

```
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```

```
source ~/.bashrc
```

```
nvm install --lts
```

```
nvm ls
```

```
sudo apt-get install nginx
```

```
sudo systemctl start nginx
```

```
sudo systemctl enable nginx
```

```
systemctl status nginx
```

```
npm install pm2@latest -g
```

```
pm2 --version
```

```
/etc/nginx/sites-available/
```

```
/etc/nginx/sites-enabled/
```

```
sudo ln -s /etc/nginx/sites-available/[name-of-your-nginx-file] /etc/nginx/sites-enabled/
```

```
sudo nginx -t
```

```
sudo systemctl reload nginx
```

```
pm2 start npm --name "tamil-matchmaking" -- start
```

```
sudo apt install snapd
```

```
sudo snap install core; sudo snap refresh core
```

```
sudo snap install --classic certbot
```

```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

```
sudo certbot --nginx
```


---

### Personal.
[signin](https://861421557251.signin.aws.amazon.com/console)
```
admin
```

```
******
```


---

### IAM & Root

- root user have full admin access.
- team members/services will use IAM users that have limited privileges.
- programmatically user don't need access to aws console & vice versa you can define this while creating and IAM.
- policies are permission attached to a IAM role. you don't have to manually define this policies aws also has predefined  templates available.
- you don't need to attach permission for each user directly, you can create a user-group and add policies to it & later add users to this user-group. also you can only attach 10 policies to user so there is a limit as well but this limit is not on user-groups.
- you can also create custom policies.
- in each template there are multiple objects of policies, each has effect, action & resource. which means if this policy active? what actions are allowed? such as reading or writing & on what resources? such as all s3 buckets or a 1 specific bucket.

### serverless vs serverfull

- in server full we are responsible for allocating resources to a server and we are rented for it.
- ASG - auto scaling group ( you can automate the resources of a server depending on the requirements )
- in server less aws is responsible for allocating/managing the resources for our code. 
- in server less we are charged only if our code is executed/innovated, for example hosting a api on server-less means that we are only charged by the incoming traffic.
- in server-less scaling is automated.
- a single code snippet is called a aws lamda function.
- each lamda function is charged on following factors
	- amount of incoming requests.
	- time duration of the code executed
- what are events and triggers?
	- triggers are basically event listeners that will invoke our events ( lamda function )
	- there can be many types of triggers such as most commonly used are api gateway where aws creates a api gateway and you can make a rest request to this url to trigger the event.
	- or you can create a trigger with alexa where you ask alexa something specific and it triggers a lamda function.
- cons are
	- server less is stateless
	- it has cold start 

### cognito

- aws cognito is a user managements service provided by aws.
- it allows multiple user authentication & authorisation strategies. User pools are primarily designed for authentication. They are user directories that provide sign-up and sign-in options for your application users.
- user pools are is all about user management
- you can manage user authentication/authorisation in 3 ways
	- hosted ui
	- **programmatically** 
		- aws amplify
		- aws sdk
	- lamda functions.
- identity pools 
	- Identity pools are focused on providing temporary AWS credentials for your app users to access other AWS services.
	- Identity pools enable your authenticated users (who may have signed in using a user pool) to obtain temporary AWS credentials. 

### s3-client (simple storage service)

- s3-client is a way to store data on a cloud computer just like you store data on you local computer.
- each s3 can have `100` buckets on a single account. we can also host static sites on s3 as s3 is just a way to store and access data from a cloud computer weather they that be a image, video or a index.html file.
- to server static content you would need to allow "Static website hosting" from bucket properties section.
- you can create a public bucket that allows access to files publicly. this means that you don't need to create a pre-signed from a IAM user that have s3 permissions enabled.
- each object(your files) on a bucket will have a public url that you can use to access them on the internet, just like serving files from a node.js server that is serving files from a public folder statically.
- if the bucket is not publicly accessible & you want to access the objects on them programmatically what you can do is that you can create a IAM role that has s3 permission enable & has programmatically access allowed. you can use this users access key and secret key to create a pre-signed URL and access the files on them.
	- you can use `aws-sdk/s3-request-presigner` for this to create pre-signed urls.

### regions, availability zones, vpc, subnets & more.


### architecture
this architecture explain how you can upload objects directly from frontend without sending files onto server.
#### this achieves 2 things
1. we are not putting unnecessary load onto server.
2. we are not exposing our env's from frontend (explained later)

![[Pasted image 20231130193937.png]]

