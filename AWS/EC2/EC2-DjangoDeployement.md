## Django application deployement using EC2 Instance
[Reference1:https://www.youtube.com/watch?v=u0oEIqQV_-E]
[Reference2:https://www.youtube.com/watch?v=wIx9c_RjUaA]
### Build Django application

### Run and check in local

### Create AWS account

### Login to AWS Console
1. Click on **launch instance**
2. Select an AMI(Amazon machine image) - **Ubuntu 18.04**
3. In next window select instance type - **t2 micro**
4. Click on **Review and Launch** 
5. Click on **launch**
6. It will pop up a new screen where you choose Create a new key pair option.
And enter Key name.
Click on Download **Key pair**, It will download the **.pem file** to your local machine.
Then Click on **Launch Instances**
7. Ensure to get satus as 2/2 checks 
8. Select instance and then click on connect option 

### Open Terminal(MAC) Command Prompt(Windows)
1. Locate your private key file 
2. Goto file location where .pem file has downloaded
3. Change pem file permissions **chmod 400 <pem file name>** --> You can also have these steps in opened window
4. Connect to instance using its public DNS copy example line - **ssh -i "python_poc.pem" ubuntu@ec2-3-94-234-195.compute-1.amazonaws.com** 
5. Paste it in terminal
6. For each time the instance restarted the public IP (ec2-3-94-234-195.compute-1.amazonaws.com)
Given by AWS change but elastic IP won’t change.
7. You have succesfully logged in with SSH client

### Install Required packages
1. sudo apt-get update
2. sudo apt-get install python3-pip -y
3. sudo pip3 install gunicorn
4. sudo apt-get install supervisor
5. sudo apt-get install nginx -y
6. sudo pip3 install django

### Transfer files from local machine to remote server using S3 or SCP commands

### To run on standalone mode
1. Open settings.py file and within allowed hosts paste public DNS within double quotes 
2. Run the application
3. Open public dns with your portnumber in browser
4. Your standalone project has deployed successfully

### Running this application inside webserver

#### Supervisor configuration:
1. **sudo vi /etc/supervisor/config.d/django.conf**
2. paste 
[program:gunicorn]
directory=/home/ubuntu/welcome
command=/usr/local/bin/gunicorn --workers 3 --bind unix:/home/ubuntu/welco
me/app.sock welcome.wsgi:application
autostart=true
autorestart=true
stderr_logfile=gunicorn.err.log
stdout_logfile=gunicorn.out.log
[group:guni]
programs:gunicorn
3. Check for location of gunicorn **which gunicorn**, Copy path
4. Paste it in conf file
5. Ensure **sudo supervisorctl reread** not to get any errors
6. **sudo supervisorctl update**
7. **sudo supervisorctl status**

#### Nginx configurations
1. Goto nginx folder **cd /etc/nginx/**
2. Create a file **sudo vi sites-available/django.conf**
3. Paste
server{
 listen 80;
 server_name ec2-54-221-184-166.compute-1.amazonaws.com;
 location / {
  include proxy_params;
  proxy_pass http://unix:/home/ubuntu/firstproject/app.sock;
 }
}
4. Modify your public dns
#### Verify NGINX config changes and restart server:
1. sudo nginx -t
2. sudo ln django.conf /etc/nginx/sites-enabled
3. sudo service nginx restart