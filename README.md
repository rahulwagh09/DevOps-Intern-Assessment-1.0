# DevOps-Intern-Assessment-1.0

#### DevOps Intern Assessment Documentation: https://docs.peerxp.com/recruitment/ops/devops-intern-assessment

Server Setup
This part of the guide will ensure all prerequisites are met for installing the Ghost-CLI.

Create a new user
Open up your terminal and login to your new server as the root user:

Login via SSH
- ssh root@your_server_ip

Create a new user and follow prompts
- adduser <user>

Add user to superuser group to unlock admin privileges
- usermod -aG sudo <user>

Then log in as the new user
- su - <user>

Update packages
Ensure package lists and installed packages are up to date.
Update package lists
- sudo apt-get update

Update installed packages
- sudo apt-get upgrade

-----------------------------------------
Install NGINX
Ghost uses an NGINX server and the SSL configuration requires NGINX 1.9.5 or higher.

### Install NGINX
- sudo apt-get install nginx

If ufw was activated, the firewall allows HTTP and HTTPS connections. Open Firewall:
- sudo ufw allow 'Nginx Full'

Install MySQL
Next, you’ll need to install MySQL to be used as the production database.

-------------------------------------------
### Install MySQL
sudo apt-get install mysql-server
On newer versions of Ubuntu, the root user created when you install MySQL will by default be configured to use socket-based authentication, meaning that only the root Unix user will be able to authenticate. Ghost does not support this kind of authentication, so you must change the root MySQL user to have a password. Run these commands to make the root user have a password:

#Enter mysql
sudo mysql
#Update permissions
ALTER USER 'root'@'localhost' IDENTIFIED WITH 'mysql_native_password' BY '<your-new-root-password>';
#Reread permissions
FLUSH PRIVILEGES;
#exit mysql
exit

-------------------------------------------
### Install Node.js
You will need to have a supported version of Node installed system-wide in the manner described below. If you have a different setup, you may encounter problems.

#Download and import the Nodesource GPG key
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

#Create deb repository
NODE_MAJOR=18 # Use a supported version
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

#Run update and install
sudo apt-get update
sudo apt-get install nodejs -y

--------------------------------------------
### Install Ghost-CLI
Ghost-CLI is a commandline tool to help you get Ghost installed and configured for use, quickly and easily. The npm module can be installed with npm or yarn.

sudo npm install ghost-cli@latest -g
Once installed, you can always run ghost help to see a list of available commands.

---------------------------------------------
### Install Ghost
Once your server is correctly setup and ghost-cli is installed, you can install Ghost itself. The following steps are the recommended setup. If you need more fine-grained control, the CLI has flags and options that allow you to break down and customise the install steps.

Create a directory
Ghost must be installed in its own directory, with a proper owner and permissions.
#Create directory: Change `sitename` to whatever you like
sudo mkdir -p /var/www/sitename

#Set directory owner: Replace <user> with the name of your user
sudo chown <user>:<user> /var/www/sitename

#Set the correct permissions
sudo chmod 775 /var/www/sitename

#Then navigate into it
cd /var/www/sitename
Run the install process

#Now we install Ghost with one final command.
ghost install

==========================================================================
## Ghost WebSite:
![Screenshot 2025-01-16 152118](https://github.com/user-attachments/assets/bacf9b44-7b52-4695-ae23-ae3b32a2e757)
## AWS Ec2:
![Screenshot 2025-01-16 152215](https://github.com/user-attachments/assets/52348fdd-8c0c-4fd6-8ed2-d30e1016b5ff)
## GitLab Pipeline:
![Screenshot 2025-01-16 154524](https://github.com/user-attachments/assets/e6e2caf3-1b44-4abb-8dc9-daa1811ce0a4)
## Job Output:
![Screenshot 2025-01-16 154727](https://github.com/user-attachments/assets/c41c501f-9993-4a68-9e0c-97f3b79778e1)

![Screenshot 2025-01-16 154703](https://github.com/user-attachments/assets/9b3a885b-cc15-440c-8937-b592e55037b2)
## Pipeline .vegaops-glci.yml
![Screenshot 2025-01-16 154549](https://github.com/user-attachments/assets/b9728365-4885-439e-9616-7cb49bb98d59)
##  GitLab Pipeline Artifact:
![Screenshot 2025-01-16 154621](https://github.com/user-attachments/assets/ffff38c0-08e4-4a90-bf9e-232124eeee5d)


