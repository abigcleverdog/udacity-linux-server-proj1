### Version 1.0

# Overview
This package is a required project of the ["Full Stack Web Developer" nanodegree][FSWD] at [Udacity]. The main objectives of this practice include configuring a linux server and deploying a web application, 'Item Catalog', on the server so that it is accessible via an IP address over the internet. 

# Result
i. The IP address: http://52.20.17.17 and SSH port: `2200`.
ii. The complete URL to the web application: http://52.20.17.17.
iii. A summary of software installed and configuration changes made:
1. The server was setup at Amazon Lightsail at the $5 tier (512MB RAM, 20GB).
2. `sudo apt-get update`, `sudo apt-get upgrade`, and `sudo apt-get autoremove` were used to keep linux packages current.
3. `sudo nano /etc/ssh/sshd_config` was used to change the ssh port to `2200` the port was also allowed in the Lightsail console (I was working on this project at different locations and some of them only allow `2222` port in their wifi service. So I opened that port as well)
4. `sudo ufw default deny incoming`, `sudo ufw default allow outgoing`, `sudo ufw allow xxx` and `sudo ufw enable` were used to configure the firewall to only listen to SSH(port 2200 and 2222), HTTP(port 80), and NTP(port 123)
5. `sudo adduser grader` was used to adde 'grader' user (there is a password for 'grader'); `sudo usermod -aG sudo grader` was used to give 'grader' superuser permission.
6. A key pair was generated using `ssh-keygen` (the privated key is provide with the submission, it has a passcode 'aaaaaa') The system was configured to only allow key based login by default.
7. `sudo apt-get install apache2` --install Apache2
8. `sudo apt-get install libapache2-mod-wsgi python-dev` --install Python mod-wsgi
9. `sudo apt-get install python` --install python
10. `sudo a2enmod wsgi` --enable wsgi
11. built the `/var/www/ItemCat/ItemCat` working directory following this guide: [How to deploy a Flask application on an Ubuntu][htdf] (I still do not quite understand what is the venv is for the later project, seems I have never needed after this step); after `sudo service apache2 restart` my web site shows the "Hello, I love Digital Ocean!" message
12. cloned over my [ItemCat] project from GitHub
13. `sudo pip install xxx` necessary packages (see package list below)
14. replace the `__init__.py` with my main app. A couple of fine tweaks: a) the original project used sqlite and this one use postgresql, so the `engine = create_engine('sqlite:///itemcat.db')` line was changed to `engine = create_engine(‘postgresql://catalog:catalog@localhost:5432/itemcat’)` in all three .py files; b) .json files were pointed to via absolute path, e.g. /var/www/ItemCat/ItemCat/xxx.json; c) IP address was added to both Google and Facebook developer console as redirect address. It was also added to the client_secret.json file; d) Flask was downgraded to 0.9 to bring Google login back to function.
iv. A list of third-party resources made use of to complete this project:
`certifi==2017.7.27.1
chardet==3.0.4
click==6.7
Flask==0.9
Flask-SQLAlchemy==2.2
httplib2==0.10.3
idna==2.5
itsdangerous==0.24
Jinja2==2.9.6
MarkupSafe==1.0
oauth2client==4.1.2
psycopg2==2.7.3
pyasn1==0.3.1
pyasn1-modules==0.0.10
requests==2.18.2
rsa==3.4.2
six==1.10.0
SQLAlchemy==1.1.12
urllib3==1.22
virtualenv==15.1.0
Werkzeug==0.12.2
`

# Functions
The functions of the ItemCat app can be found in the original GitHub repo [README]

# How to use
Open the app in a browser at http://52.20.17.17.

# License
MIT

***********************
  [FSWD]: <https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004>
  [Udacity]: <https://www.udacity.com>
  [git]: <https://www.virtualbox.org/wiki/Downloads>
  [vb]: <https://www.virtualbox.org/wiki/Downloads>
  [vag]: <https://www.vagrantup.com/downloads>
  [htdf]: <https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps>
  [ItemCat]: <https://github.com/abigcleverdog/udacity-auth-course-proj1>
  [README]: <https://github.com/abigcleverdog/udacity-auth-course-proj1/blob/master/README.md>