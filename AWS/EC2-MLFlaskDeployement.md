## Machine Learning Flask application deployement using EC2 Instance
[Reference:https://www.youtube.com/watch?v=oOqqwYI60FI&list=PLZoTAELRMXVOAvUbePX1lTdxQR8EY35Z1&index=7]
### Build flask application

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

### Download putty and puttygen 
 putty
 puttygen(only for windows)
 WinSCP(only for windows)

### Generate private key using puttyGen
#### For windows
1. Open puttygen
2. Click on load, Select all files
3. Select .pem file which you have downloaded, click on save private key
4. Click yes, and specify name as **mykey.ppk** and file type as all files then save.

#### For mac
1. Open terminal
2. Run **puttygen mykey.pem -o mykey.ppk**

Note: **puttygen key.ppk -O private-openssh -o key.pem** to convert file from .ppk to .pem file

#### For windows
1. Open WinSCP
2. Copy Public DNS from EC2 instance and paste in host field
3. Enter user name (ex:ubuntu)
5. Click advanced
6. On left window, click on Authentication
7. In private key field, select your .ppk file which you have recentry generated
8. Click open, ok, login
9. Click yes, remote server connection will be established succesfully
10. Drag and drop required files 
11. Open putty
12. Enter host name and specify a session name, then click SSH on left panel and select Auth
13. Select ppk file and click open
14. Specify username as ubuntu

#### For mac
1. Goto EC2 instance
2. Copy file permissions command, paste in terminal
3. Copy command to connect to remote server which is specified in example, paste it in terminal
4. Remote server will be connected successfully
3. Transfer required files from local to remote server using below required command
 

#### Basic commands for communication between local and remote server on mac 
1. Open two terminals, one for local and other for remote server
2. To copy file from local system to remote server on home directory 
**scp -i MLModelPragathi.pem f1.txt ubuntu@ec2-54-163-38-111.compute-1.amazonaws.com:**
3. To copy folder from local system to remote server 
**scp -i MLModelPragathi.pem -r foldername ubuntu@ec2-54-163-38-111.compute-1.amazonaws.com:**
4. To copy files from local system to remote server on a specific directory 
**scp -i MLModelPragathi.pem f1.txt ubuntu@ec2-54-163-38-111.compute-1.amazonaws.com:<dirname>/**
5. To copy file from remote server to local system on present directory 
**scp -i MLModelPragathi.pem f1.txt ubuntu@ec2-54-163-38-111.compute-1.amazonaws.com:<filename> .**
6. To copy folder from remote server to local system on present directory 
**scp -i MLModelPragathi.pem -r foldername ubuntu@ec2-54-163-38-111.compute-1.amazonaws.com:foldername .**

### After successfull login into remote server
1. Ensure all required files should be present
2. Install required libraries
    a. sudo apt-get update
    b. sudo apt-get install python3-pip
    c. pip3 install -r requirements.txt
3. In EC2 console, goto security groups 
4. Create security group, To allow all traffic select add rule and specify all traffic and anywhere
5. Provide a name, description and click on create, Notedown security group id
6. Goto Network interfaces tab, select your network and click on action then, change security group
7. Add recently created security group and save.
8. Open terminal
9. Run python file **python3 app.py**
10. Open ec2 copy public DNS, paste in browser with specified port number
11. Your application gets deployed successfully