# Note step by step deploy on amazon web service

### Create EC2 instance on AWS
1. Create EC2 (Elastic Compute Cloud) instance.
2. Generate new key pair (if dont have before).
3. Download this key pair and keep it (top secret).
4. Waiting until instance state change to running.
5. Done.

### Configuration ssh from local to server
1. ssh to server first time
```
  chmod 400 <path_to_key_pair>
  ssh -i <path_to_key_pair> <user>@<public_DNS>
```

2. generate ssh public key on local
```
  ssh-keygen -t rsa -C <local_name>
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

6. Create `config` ssh file
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

7. ssh to server
```
  ssh <user_to_ssh>
```
