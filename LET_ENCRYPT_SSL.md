## Config Let's Encrypt SSL on server

1. Clone Let's Encrypt repository
```
git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
```

2. Issue SSL Let's Encrypt
```
  sudo service nginx stop
  sudo mkdir /opt/letsencrypt/certbot-auto
  sudo /opt/letsencrypt/certbot-auto certonly --standalone
  -> input your email -> type A -> input non-www and www domain (sub-domain)
  done
```

3. Config Nginx
  * Create DH parameters 2048 bit

```
  sudo mkdir /etc/nginx/ssl
  sudo openssl dhparam 2048 -out /etc/nginx/ssl/dhparam.pem
```

  * Edit your config
```
  sudo vi /etc/nginx/conf/default.conf

  server {
    listen 80;
    listen 443 ssl default_server;

    server_name <your_domain> www.<your_domain>;

    # SSL
    ssl_certificate /etc/letsencrypt/live/moon-hai.site/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/moon-hai.site/privkey.pem;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_ciphers EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;

    # Improve HTTPS performance with session resumption
    ssl_session_cache shared:SSL:50m;
    ssl_session_timeout 1d;

    # DH parameters
    ssl_dhparam /etc/nginx/ssl/dhparam.pem;
    # Enable HSTS
    add_header Strict-Transport-Security "max-age=31536000" always;

    root /cv;
    index index.html index.htm;

    # redirect to https
    if ($scheme = http) {
      return 301 https://$server_name$request_uri;
    }

    error_page 404 /error_404.html;
  }
```

  * Check nginx and restart
```
  sudo nginx -t
```
![nginx, nginx check](/assets/images/nginx_check.png)

4. Change inbound setting on EC2
```
  Go to EC2 dashboard
  Add Inbound settings: HTTPS
```
![inboud, inboud rules](/assets/images/inboud_rules_https.png)

5. Done

## Auto register when SSL certificate expired
```
  /opt/letsencrypt/certbot-auto renew --pre-hook 'service nginx stop' --post-hook 'service nginx start'
```

## Auto register with crontab
```
  EDITOR=vi crontab -e

  30 2 * * * /opt/letsencrypt/certbot-auto renew --pre-hook "service nginx stop" --post-hook "service nginx start" >> /var/log/le-renew.log
  :wq
```
![crontab, add crontab](/assets/images/crontab_add.png)
