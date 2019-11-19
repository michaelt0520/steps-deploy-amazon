## Basic config nginx

1. install nginx
```
  sudo amazon-linux-extras install nginx1.12(nginx1)
```

2. create folder of project
```
  sudo mkdir /<name_of_folder>
  fetch project to this folder
```

3. config nginx
```
  cd /etc/nginx
  sudo rm -rf /default.d
  sudo vi conf.d/default.d

  server {
    listen 80;
    server_name <server_name>;

    root <path_to_project_foler>;
    index index.html index.htm;
    error_page 404 /error_404.html;
  }

  :wq
```

4. Check nginx config
```
  sudo nginx -t
```

5. Restart nginx
```
  sudo service nginx restart
```

## Enabled HTTP on EC2
```
  Check Security groups of your Instance
  Choose Security Groups of NETWORK & SECURITY in the side bar
  On SG of instace, add more Inbound rules is HTTP
  Save
```
![inboud, inboud rules](/assets/images/inboud_rules_https.png)
