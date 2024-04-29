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
