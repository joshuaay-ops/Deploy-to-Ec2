# Deploy-to-Ec2


Domain
Bought a domain on Cloudflare.

# EC2 instance
Launched an EC2 instance via the AWS Console. Set the security group to allow inbound traffic on ports 22 (SSH) and 80 (HTTP).

Installed NGINX
Connected to the instance via SSH and installed NGINX:

```bash
sudo dnf install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

# DNS setup
I created an A record in cloudflare which points the domain to the ec2 instnaces ip address. Which allows the domain name to load the server instead of using the ip directly.

Verified it worked
Waited for DNS to propagate. and checked for connectivity, returned back 200 OK.
```bash
curl -I https://jay-ops.co.uk
```

<img width="383" height="107" alt="image" src="https://github.com/user-attachments/assets/c69adc82-3f3b-4444-9b7d-8f3da084a165" />




<img width="1893" height="939" alt="image" src="https://github.com/user-attachments/assets/d339177c-85ca-4098-95fb-3ccb49141a8a" />













# Set up https
Used the command below to install Certbot tool and point it to the domain to enable Letsencrypt.

```bash
sudo dnf install certbot python3-certbot-nginx -y
sudo certbot --nginx -d jay-ops.co.uk
```
<img width="446" height="125" alt="image" src="https://github.com/user-attachments/assets/c201b371-fa4d-4e61-9868-6149130b5a42" />

# Domain Secured

<img width="1884" height="880" alt="image" src="https://github.com/user-attachments/assets/6e4a83aa-07c2-40ea-8496-9e64398a17a3" />

Notes -
Waiting a few minutes for the dns propagation longer than expected.
Had to research to use dnf instead of yum/amazon-linux-extras since Amazon Linux 2023 dropped the old extras tool.
Changed the DNS record and set it to dns only in Cloudflare (not proxied) to keep things simple for testing.
I secured the site by using https using the ssl certificate from LetsEncrypt.

AWS EC2, NGINX, Cloudflare DNS
