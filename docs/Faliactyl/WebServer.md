---
sidebar_position: 4
---

## Setting Up Nginx
The Nginx web server will allow us to use a custom domain name and apply SSL to it.

First, we need to make sure you have `Nginx` and `certbot` installed:
```bash
sudo apt install nginx
sudo apt install certbot
sudo apt install -y python3-certbot-nginx
```

Now you can install your SSL certificate:
```bash
systemctl start nginx
certbot certonly --nginx -d <Faliactyl_Domain>
```

Make sure to replace `<Faliactyl_Domain>` with your domain name. If you have done this correctly you should see something similar to the following:
```
IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/your.faliactyl.domain/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/your.faliactyl.domain/privkey.pem
   Your cert will expire on date. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```
If what you saw isn't similar to what you saw in your server, we recommend you ask for support on our [Discord Server](https://discord.gg/dJqrJAEksC).

Next, if everything's going correctly, you need to go to the Nginx sites directory and create a configuration file:
```bash
cd /etc/nginx/sites-available
nano faliactyl.conf
```

Now paste the following into the file. Make sure to replace `<DOMAIN>` and `<PORT>` with your Faliactyl domain and the port Faliactyl is running on.
```conf
server {
  listen 80;
  server_name <DOMAIN>;
  return 301 https://$server_name$request_uri;
}
server {
  listen 443 ssl http2;

  server_name <DOMAIN>;
  ssl_certificate /etc/letsencrypt/live/<DOMAIN>/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/<DOMAIN>/privkey.pem;
  ssl_session_cache shared:SSL:10m;
  ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers  HIGH:!aNULL:!MD5;
  ssl_prefer_server_ciphers on;

  location / {
    proxy_pass http://localhost:<PORT>/;
    proxy_buffering off;
    proxy_set_header X-Real-IP $remote_addr;
  }
  
  location /afkwspath {
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_pass "http://localhost:<PORT>/afkwspath";
  }
}
```
After we've setup the main config file, we'll need to symlink it to sites-enabled:
```bash
sudo ln -s /etc/nginx/sites-available/faliactyl.conf /etc/nginx/sites-enabled/faliactyl.conf
```

  Once you have edited, saved, and symlinked your configuration file, restart Nginx with `systemctl restart nginx` and restart Faliactyl. You should see it running on that domain with SSL!
  
## Starting Faliactyl

First we need to install pm2:
```
npm install pm2 -g
```
Now you need to go to the dashboard directory and use:
```
pm2 start index.js
```