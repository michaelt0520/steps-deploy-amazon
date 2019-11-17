# Note step by step deploy on amazon web service

### Create EC2 instance on AWS
1. Create EC2 (Elastic Compute Cloud) instance.
2. Generate new key pair (if dont have before).
3. Download this key pair and keep it (top secret).
4. Waiting until instance state change to running.
5. Done.

### Configuration ssh from local to server
1. generate ssh public key on local
```
  ssh-keygen -t rsa -C <local_name>
```

2. ssh to server first time
```
  chmod 400 <path_to_key_pair>
  ssh -i <path_to_key_pair> <user>@<public_DNS>
```

3. create user (S)
```
  sudo useradd <name_of_user>
  sudo passwd <name_of_user>
  enter password and confirm password
```

4. setup full role for new user (S)
```
  sudo su - <name_of_user>
  vi /etc/sudoers
  add <name_of_user> ALL=(ALL) ALL
  :wq
```

5. setup ssh key authentication (S)
```
  mkdir .ssh
  sudo chmod 700 .ssh
  vi ~/.ssh/authorized_keys
  add ssh public key of local Mac (on ~/.ssh/id_rsa.pub)
  :wq
  sudo chmod 600 ~/.ssh/authorized_keys
```

6. set true for password authentication each times ssh
```
  sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
  sudo systemctl restart sshd
```

7. Create `config` ssh file
  * ssh/config file
  ```
    vi ~/.ssh/config
  ```

  * add config
  ```
    Host <Public_DNS_or_Public_Ip>
    User <user_to_ssh>
    IndentityFile <path_to_key_pair_OR_path_to_private_ssh_key>
  ```

8. ssh to server
```
  ssh <user_to_ssh>
```

### Config nginx on server
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

### Setup https on nginx

### Enabled HTTP on EC2
```
  Check Security groups of your Instance
  Choose Security Groups of NETWORK & SECURITY in the side bar
  On SG of instace, add more Inbound rules is HTTP
  Save
```

### Authorized server with github account
1. Generate ssh public key on server (step above)
2. Open Github account -> Settings -> SSH & GPG keys -> create new ssh key -> paste rsa_key.pb
3. Done
