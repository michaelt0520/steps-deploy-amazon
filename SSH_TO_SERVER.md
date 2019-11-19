## Config ssh to server

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
![sudoers, sudoers](/assets/images/sudoers.png)

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
