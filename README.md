# Note step by step deploy on amazon web service

### Create EC2 instance on AWS
1. Create EC2 (Elastic Compute Cloud) instance.
2. Generate new key pair (if dont have before).
3. Download this key pair and keep it (top secret).
4. Waiting until instance state change to running.
5. Done.

### Configuration ssh from local to server
Follow [this](https://github.com/moon-hai/steps-deploy-amazon/blob/master/SSH_TO_SERVER.md).

### Config nginx on server
Follow [this](https://github.com/moon-hai/steps-deploy-amazon/blob/master/BASIC_NGINX.md).

### Setup https on nginx
1. Point domain to aws ec2
Follow [this](https://github.com/moon-hai/steps-deploy-amazon/blob/master/SETUP_DOMAIN.md).

2. Config Let's Encrypt SSL on server
Follow [this](https://github.com/moon-hai/steps-deploy-amazon/blob/master/LET_ENCRYPT_SSL.md).

### Authorized server with github account
1. Generate ssh public key on server (step above)
2. Open Github account -> Settings -> SSH & GPG keys -> create new ssh key -> paste rsa_key.pub
3. Done
