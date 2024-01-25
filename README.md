1.	Create a new instance.
•	Application and OS Images (Amazon Machine Image) – select Amazon Linux and 64-bit Architecture, AMI ID.
•	Create a New Key Pair with a random name and select. ppk as private key file format. Click on Create key pair (file fill gets auto download).
•	Check to Allow SSH traffic from & Allow HTTPS traffic from the internet.
•	Click on launch instance.
2.	Connection Instance with Putty
•	Download Putty and extract it.
•	Click on top of the instance Id from Newley created instance.
•	Copy the Public IPv4 DNS address and paste it in the putty Host Name (or IP address)
•	Expand SSH left panel in putty.
•	Expand the Auth panel under SSH in Putty
•	Click on Credentials
•	Click on browse for the Private key file for authentication. 
•	Upload the ppk file which was downloaded initially on creating the instance.
•	Click on open.
•	Click on the accept button if modal windows open with the title of PuTTY Security Alert
•	Login as - ec2-user
•	Message - Authenticating with public key and now it got connected.
3.	Run this command: 
•	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash (It downloads and executes a script from the specified URL)
•	sudo yum update.
•	sudo systemctl status nginx (It shows nginx running status)
•	sudo systemctl start nginx (To start nginx)
•	sudo vim /etc/nginx/nginx.conf (To edit the configuration of nginx)
•	Click on I to write the method and paste the below lines!

location  {
        proxy_pass http://localhost:3210;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
4.	Run this command  :  
•	sudo systemctl restart nginx ( To restart nginx) after that check the nginx status, it needs to active (running) state
•	sudo yum install git (install Git)
•	sudo git clone https://github.com/fayazahamedd/reactPortFolio.git
5.	 Run the commands:
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ cd ..
•	[ec2-user@ip-172-31-4-163 ~]$ cd ..
•	[ec2-user@ip-172-31-4-163 home]$ ls
•	ec2-user
•	[ec2-user@ip-172-31-4-163 home]$ cd ec2-user/
•	[ec2-user@ip-172-31-4-163 ~]$ sudo chmod -R 777 reactPortFolio/
•	[ec2-user@ip-172-31-4-163 ~]$ cd reactPortFolio/
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ sudo yum install -y nodejs
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ sudo npm install -g npm@10.3.0
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ npm install -force
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ sudo yum install xdg-utils
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ npm run dev
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ npm run build	
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ sudo npm install pm2 -g
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ pm2 start npm --name "reactPortFolio" -- run dev.
•	[ec2-user@ip-172-31-4-163 reactPortFolio]$ pm2 status(To check the status of pm2)
6.	Copy the Public IPv4 address from the instance summary paste it in Chrome and finally web app starts running.
