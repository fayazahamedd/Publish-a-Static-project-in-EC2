# React Portfolio Deployment on AWS EC2

This repository provides a complete guide to deploy a **React application** on an **AWS EC2 instance** with **NGINX**, **PM2**, and automation for seamless startup. The steps cover instance creation, SSH connection, environment setup, deployment, and troubleshooting.

---

## Overview

Welcome to the React Portfolio deployment guide! This setup demonstrates how to:

- Create and configure an EC2 instance
- Install Node.js, NGINX, and PM2
- Clone and run a React application
- Automate processes for startup
- Associate Elastic IP for a static web address

---

## 1. Create a New EC2 Instance

1. Launch a new instance:
   - Select **Amazon Linux** with **64-bit Architecture** (AMI ID).  
   - Create a **new key pair** (.ppk format) and download it.  
   - Allow **SSH** and **HTTPS** traffic from the internet.  
   - Click **Launch instance**.

2. Verify the instance is running in the EC2 console.

---

## 2. Connect to EC2 Using PuTTY

1. Download and extract **PuTTY**.  
2. Copy the **Public IPv4 DNS** from the instance summary.  
3. Open PuTTY and paste the IP into **Host Name (or IP address)**.  
4. Navigate to **SSH → Auth → Credentials → Browse** and upload the `.ppk` private key.  
5. Click **Open** and accept the security alert.  
6. Login as:  
   ```bash
   ec2-user
3. Setup NGINX and Node Environment

Run the following commands:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
sudo yum update -y
sudo systemctl status nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo vim /etc/nginx/nginx.conf


Add this block in NGINX configuration:

location {
    proxy_pass http://localhost:3210;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}


Restart NGINX:

sudo systemctl restart nginx
sudo systemctl status nginx

4. Clone React Repository
sudo yum install git -y
git clone https://github.com/fayazahamedd/reactPortFolio.git
cd reactPortFolio/
sudo chmod -R 777 reactPortFolio/
sudo yum install -y nodejs
sudo npm install -g npm@10.3.0
npm install --force
sudo yum install xdg-utils -y
npm run dev
npm run build
sudo npm install pm2 -g
pm2 start npm --name "reactPortFolio" -- run dev
pm2 status


Open the Public IPv4 address in your browser to verify the web app is running.

5. Automate Instance Startup

Install cronie for scheduled tasks:

sudo yum install cronie -y
sudo systemctl enable crond.service
sudo systemctl start crond.service


Setup PM2 to start on reboot:

pm2 stop all
pm2 kill
cd /home/ec2-user/reactPortFolio
/usr/local/bin/pm2 start npm --name "reactPortFolio" -- run dev
crontab -e


Add the following line in crontab:

@reboot cd /home/ec2-user/reactPortFolio && /usr/local/bin/pm2 start npm --name "reactPortFolio" -- run dev


Switch to root and reboot:

sudo su -
reboot

6. Allocate Elastic IP

Navigate to Elastic IPs in the AWS console.

Click Allocate Elastic IP address → Allocate.

Associate the Elastic IP to your instance.

Verify that the Public IPv4 address updates to the Elastic IP.

Paste the Elastic IP in your browser to access the application.

7. Troubleshooting

Check NGINX errors:

sudo journalctl -xe | grep nginx


View PM2 logs:

pm2 log


Ensure NGINX is active and PM2 is running your React app correctly.

8. Notes

Make sure to maintain the .ppk key safely for SSH access.

Use Elastic IP for a stable public address.

Always test PM2 and NGINX after reboot to ensure services are running.

THE END
