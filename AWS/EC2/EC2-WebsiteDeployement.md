## Web application deployement using EC2 Instance
[Reference:https://www.youtube.com/watch?v=hOYg-ClP84g]

### Build a website
### Zip that folder

### Create AWS account

#### Upload code files to S3 bucket
1. Login to AWS Console
2. Open S3 service, Create a bucket
3. Upload zipped folder into it
4. Make bucket public, Goto permissions tab and uncheck public access then save
5. Make object public, Select folder, click actions and make public

#### Launch EC2 instance
1. Click on **launch instance**
2. Select an AMI(Amazon machine image) - **Linux 2 AMI**
3. In next window select instance type - **t2 micro**
4. In Security group, add HTTP and 80 port
5. Click on **Review and Launch** 
6. Click on **launch**
7. It will pop up a new screen where you choose Create a new key pair option.
And enter Key name.
Click on Download **Key pair**, It will download the **.pem file** to your local machine.
Then Click on **Launch Instances**
8. Ensure to get satus as 2/2 checks 
9. Select instance and then click on connect option 

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
1. To run as root **sudo su**
2. Install epel packages **sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm**
2. Update EC2 instance **yum update -y**
3. Install apache **yum install httpd -y**
4. Change directory to **cd /var/www/html**
5. Copy zip folder from S3 to EC2 instance **wget <S3 Object URL>**
6. List files to ensure copied files **ls**
7. Unzip using **unzip <Zipped file name>**
8. Move files from folder to present working folder**mv MyPortfolio/* .**
9. Start service using **service httpd start**
10. Open browser and copy paste public dns, your website has deployed successfully