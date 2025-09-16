# 🚀 React Portfolio Deployment on AWS EC2

This repository provides a complete guide to deploying a **React application** on an **AWS EC2 instance** using **NGINX**, **PM2**, and automated startup configuration. It covers everything from instance creation to troubleshooting.

---

## 📋 Overview

This guide walks you through:

- Creating and configuring an EC2 instance
- Installing Node.js, NGINX, and PM2
- Cloning and running a React application
- Automating startup with crontab
- Associating an Elastic IP for a static web address

---

## 🖥️ 1. Create a New EC2 Instance

1. Launch a new EC2 instance:
   - Select **Amazon Linux 64-bit (x86)** AMI
   - Create and download a **new key pair** in `.ppk` format
   - Allow **SSH** and **HTTPS** traffic
   - Click **Launch Instance**

2. Confirm the instance is running in the EC2 dashboard.

---

## 🔐 2. Connect to EC2 Using PuTTY

1. Download and open **PuTTY**
2. Copy the **Public IPv4 DNS** from your instance
3. In PuTTY:
   - Paste the IP into **Host Name**
   - Go to **SSH → Auth → Browse** and select your `.ppk` key
4. Click **Open** and login as:
   ```bash
   ec2-user

## ⚙️ 3. Setup NGINX and Node Environmen

    ```bash
      curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
      sudo yum update -y
      sudo yum install nginx -y
      sudo systemctl enable nginx
      sudo systemctl start nginx
      
   Edit NGINX config

      ```bash 
         sudo vim /etc/nginx/nginx.conf

   Add this block inside the server block:

      ```bash 
         location / {
         proxy_pass http://localhost:3210;
         proxy_http_version 1.1;
         proxy_set_header Upgrade $http_upgrade;
         proxy_set_header Connection 'upgrade';
         proxy_set_header Host $host;
         proxy_cache_bypass $http_upgrade;
         }

   Restart NGINX:

      ```bash
         sudo systemctl restart nginx

### 📦 4. Clone and Run React App

    ```bash 

       sudo yum install git -y
         git clone https://github.com/fayazahamedd/reactPortFolio.git
         cd reactPortFolio/
         sudo chmod -R 777 .
         sudo yum install -y nodejs
         sudo npm install -g npm@10.3.0
         npm install --force
         sudo yum install xdg-utils -y
         npm run dev
         npm run build
         sudo npm install pm2 -g
         pm2 start npm --name "reactPortFolio" -- run dev
         pm2 status
         
##🔄 5. Automate Instance Startup

      ```bash
      
      sudo yum install cronie -y
      sudo systemctl enable crond.service
      sudo systemctl start crond.service

setup PM2 to start on reboot:
    
    ```bash
    
      pm2 stop all
      pm2 kill
      cd /home/ec2-user/reactPortFolio
      /usr/local/bin/pm2 start npm --name "reactPortFolio" -- run dev
      crontab -e


Add this line to crontab:

    ```bash
       @reboot cd /home/ec2-user/reactPortFolio && /usr/local/bin/pm2 start npm --name "reactPortFolio" -- run dev

      Reboot:
      sudo su -
      reboot



### 🌐 6. Allocate Elastic IP

   - Go to Elastic IPs in AWS Console
   - Click Allocate Elastic IP address → Allocate
   - Associate the IP with your EC2 instance
   - Use the Elastic IP in your browser to access the app

### 🛠️ 7. Troubleshooting

    ```bash
    
      Check NGINX errors:
      sudo journalctl -xe | grep nginx


View PM2 logs:

    ```bash pm2 log


Ensure both NGINX and PM2 are active and serving your React app.

### 📝 8. Notes
   - Keep your .ppk key secure for SSH access
   - Use Elastic IP for a consistent public address
   - Always verify PM2 and NGINX after reboot

✅ Done!
Your React portfolio is now live on AWS EC2 with a robust and automated setup. Happy coding!


