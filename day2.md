
A Debian based OS e,g Ubuntu system is recommended for the Odoo server, though Odoo can run on a variety of operating systems, so why pick Debian at the expense of other operating systems? Because Debian is considered the reference deployment platform by the Odoo team; it has the best support.  It will be easier to find help and additional resources if we work with Debian/Ubuntu. It's also the platform that the majority of developers work on and where most deployments are rolled out.

#####To install Odoo we only need these following applications:
1. Python
2. PostgreSQL
3. Odoo and all the required libraries
However, this could prove to be very challenging at first, so it is adviceable to make use of a virtual machine running Debian or Ubuntu Server(Ubuntu preferably).

#### Creating a user account for Odoo
Our first task is to create an Odoo user on our newly installed __OS__ , many people considered it bad practice to work as super user . In particular, the Odoo server will refuse to run if you start it as the __super user__ .

```bash
    >>> apt-get update && apt-get upgrade # Install system updates
    # This is meant for elivationg the user access right.
    >>> apt-get install sudo # Make sure 'sudo' is installed, 
```
The next step is to create a new user __odoo__ user
```bash
    >>> useradd -m -g sudo -s /bin/bash odoo # Create an 'odoo' user with sudo power
    >>> passwd odoo # Ask and set a password for the new user
```
We can any username/name we want. The __-m__ flag/option/argument ensures that the user's home directory is created. The __-g__ flag/option/argument adds the user to the sudoers list so it can run commands as __super user__ . The -s bin/bash  option sets the default shell to *bash*. Now we should be able to login and using the new user's credentials and set up Odoo.
 
#### Installing Odoo from the source
It is more convenient for module developers as the Odoo source is more easily accessible than using packaged installation. It also makes starting and stopping Odoo more flexible and explicit than the services set up by the packaged installations, and allows overriding settings using command-line parameters without needing to edit a configuration file.

As developers, we will prefer installing them directly from the GitHub repository. This will give us more control over versions and updates. 
To make thing clean and organized, let us create a folder called __odoo10__ in our home directory and change into the directory.
```bash
    >>> sudo apt-get update && sudo apt-get upgrade #Install system updates
    >>> sudo apt-get install git # Install Git
    >>> sudo apt-get install npm # Install NodeJs and its package manager
    >>> curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
    >>> sudo apt-get install -y nodejs
    >>> sudo npm install -g less less-plugin-clean-css #Install less compiler
```
Once we are through installing all the above packages, the next task is to get Odoo from the source __Github__ and install all its dependencies.
```bash
    >>> pwd # This is to confirm that we are in the right directory(Odoo10).
    >>> cd ~/odoo10 # Go into our working directory if not already in Odoo10 directory
    >>> git clone https://github.com/odoo/odoo.git -b 10.0 --depth=1 # Get Odoo source code from github
```
The git  __-b 10.0__ tells Git to explicitly download the 10.0 branch of Odoo. The __--depth=1__ option tells Git to download only the last revision, instead of the full change history, making the download smaller and faster. To start an Odoo server instance, just run:
```bash
    >>> ls # list all the files and directory current directory
    >>> # change to the Odoo source directory
    >>> # Download all the Odoo required system packages
    >>> sudo apt-get install python-pip python-dev build-essential
    >>> sudo pip install --upgrade pip 
```
Next, download system libraries needed for Odoo to run
```
    >>> sudo apt-get install python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip  python-passlib python-decorator gcc python-dev mc bzr python-setuptools python-markupsafe python-reportlab-accel python-zsi python-yaml python-argparse python-openssl python-egenix-mxdatetime python-usb python-serial lptools make python-pydot python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests python-xlsxwriter python-suds python-psycogreen python-ofxparse python-gevent
```
Now, let us install missing dependencies using python pakage management, in our odoo source diretory run this command, it will install python interface to all the above system pakages.
```python
    sudo pip install -r requirements.txt
```
Odoo is now ready but not finally ready, from our directory run this command: 
By default, Odoo instances listen on port __8069__ , so if we point a browser to
__our-server-ip:8069__ , we will reach the instance. When we access it for
the first time, it shows us an assistant to create a new database, as shown in the following
screenshot:
```bash
    ./odoo-bin #This will launch/start odoo server
```
![Odoo Running](img/Screenshot-2018-1-23 Odoo.png  "Odoo Running")

But wait, we are yet to complete the installation, but we are almost through, we need to set up our database sever(postgresSQL) before we can make use ofour Odoo. let us install the database server quikly.

```bash
    >>> touch /etc/apt/sources.list.d/pgdg.list # use sudo if you don't have access right to create the file
    >>> deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
    >>> wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    >>> sudo apt-get update 
    >>> sudo apt-get install postgresql-9.6
```
 The repository contains many different packages including third party addons. The most common and important packages are (substitute the version number as required):

* postgresql-client-9.6 - client libraries and client binaries
* postgresql-9.6 - core database server
* postgresql-contrib-9.6 - additional supplied modules libpq-dev - libraries and headers for C language frontend development
* postgresql-server-dev-9.6 - libraries and headers for C language backend development
* pgadmin3 - pgAdmin III graphical administration utility


For us to be able to create a new database, our user must be a PostgreSQL user. The following command creates a PostgreSQL superuser for the current Unix user, though it bad practice to use superadmin for this purpose, but for leaning sake we shall.
```bash
    >>> sudo createuser --superuser $(whoami) # Create postgres user using current log in user.
```
To change the database login for our newly created role/user
```SQL
    ALTER ROLE davide WITH PASSWORD '****';
```
To create a new database, use the __createdb__ command. Let's create a __demo__ database:
```bash
    >>> createdb demo
```
To initialize this database with the Odoo data schema, we should run Odoo on the empty database using the __-d__ option:
```bash
    >>> ~/odoo-dev/odoo/odoo-bin -d demo
```
This will take a couple of minutes to initialize a __demo__ database, and it will end with an INFO log message, __Modules loaded.__