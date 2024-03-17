# Setting Up AWS EC2 Instance for React Portfolio Deployment

This guide outlines the steps to set up an Amazon EC2 instance for deploying a React portfolio. Follow these instructions to create a new instance, connect to it using PuTTY, configure nginx, and deploy the React portfolio.

## 1. Create a New Instance

- Choose Amazon Linux and 64-bit Architecture for the AMI.
- Create a new Key Pair with a random name and download the `.ppk` private key file.
- Allow SSH and HTTPS traffic from the internet.
- Launch the instance.

## 2. Connect Instance with PuTTY

- Download and extract PuTTY.
- Copy the Public IPv4 DNS address of the instance.
- Paste the DNS address in the Host Name (or IP address) field in PuTTY.
- Configure SSH and Authentication settings by providing the private key file.
- Open the connection and authenticate as `ec2-user`.

## 3. Run Commands

Run the following commands on the connected instance:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
sudo yum update
sudo systemctl status nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo vim /etc/nginx/nginx.conf


location / {
    proxy_pass http://localhost:3210;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
## Run this command
sudo systemctl restart nginx
sudo yum install git


cd ~
sudo chmod -R 777 reactPortFolio/
cd reactPortFolio/
sudo yum install -y nodejs
sudo npm install -g npm@10.3.0
npm install -force
sudo yum install xdg-utils


```bash
