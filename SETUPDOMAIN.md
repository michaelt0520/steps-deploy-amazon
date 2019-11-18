## Setup domain with GoDaddy and AWS EC2

### Buy a domain on GoDaddy
[GoDaddy](https://vn.godaddy.com/).
![domain, domain on godaddy](/assets/images/domain.png)

### Setup Route 53 on AWS
1. Create Hosted Zone on Route 53
```
  Choose Route 53 service
  Choose Hosted zones
  Create Hosted Zone
  Input your Domain Name -> Type: Public Hosted Zone -> Create
```

2. Create Record Set
```
  Choose Create Record Set
  name: <your_domain> -> Type: A - IPv4 address -> Alias: No -> Value: <your_ipv4_public_add_on_ec2>
  Save Record Set
```
![record, record set on Hosted Zone](/assets/images/record_set_01.png)

```
  Choose Create Record Set
  name: www.<your_domain> -> Type: A - IPv4 address -> Alias: Yes -> Alias Target: moon-hai.site.
  Save Record Set
```
![record, record set on Hosted Zone](/assets/images/record_set_02.png)

3. Edit NS TTL
```
  Choose NS moon-hai.site
  Edit TTL to 300s
  Save Record Set
```
![record, record set on Hosted Zone](/assets/images/ns_ttl.png)

### Setup Domain Name Server on GoDaddy
1. DNS Management
```
  Choose DNS Management
  Choose Edit -> Custom
  Add 4 value on Name Server (Route 53 - AWS) to this
  Save
```
![record, record set on Hosted Zone](/assets/images/ns_godaddy.png)

2. Done
```
  Waiting at least 5 mins to domain update infomation
```
