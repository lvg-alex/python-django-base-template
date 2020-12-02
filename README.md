# python-django-base-template

It shows the sequence of actions that must be performed in order to install all the necessary packages on a clean Debian operating system and prepare the system for working with Django.

## Step 1. Debian Server Set Up for Django Instructions
Shows how to set up a clean Debian server for Python and Django projects. A secure SSH connection is implemented, packages are installed from Debian repositories and source code, and the Debian server is prepared to work with Django.

1. Launch cmd.exe () or powershell.exe.
```bash
cmd
```

2. Create user, setup SSH.
Configure a connection to a Debian VM using SSH. Create a new key using the ssh-keygen command. Execute the command:
```bash
ssh-keygen -t rsa -b 2048
```
After executing the command, specify the names of the files where the keys will be saved and enter the password for the private key. You will need to enter a keyword.
Keys are created in the directory C:\Users\<username>\ssh\. The public part of the key will be saved in a file named <key_name>.pub. The default name is id_rsa.
Save the generated key pair on the local machine.

3. Restart SSH server, change `www` user password:
```bash
sudo service ssh restart
``` 
4. Set the password for the user "www".
```bash
sudo passwd www
``` 

5. Connect through SSH to remote Debian server.
Use the command line to connect to the VM:
```bash
C:\WINDOWS\system32>ssh <user name>@XXX.XXX.XXX.XXX
```
For example, for the user "www" and the ip address "127.0.0.1" will look like (`ssh www@127.0.0.1`).

6. Update repositories and install some initial needed packages:
```bash
sudo apt-get update
sudo apt-get install -y vim mosh tmux htop git curl wget unzip zip gcc build-essential make
```
Brief information about packages `vim – advanced text editor;
mosh – improved ssh, automatically reconnects the connection on the mobile device;
tmux – terminal multiplexer;
htop – process monitor;
git – repository;
curl – for uploading external files, you can use it during testing;
wget – for uploading external files;
unzip – обертка для работы с zip-архивом;
zip – wrapper for working with a zip archive;
gcc – the compiler to build the sources;
build-essential – a compiler for building sources is required for building from sources;
make – required for building from source`.

7. Configure SSH so that the user <user name> can connect via SSH.
```bash
sudo vim /etc/ssh/sshd_config
``` 
To add to the configuration file
```sshd_config
    AllowUsers <user name>
    PermitRootLogin no
    PasswordAuthentication no
``` 
Brief information about packages `AllowUsers <user name> – the user will have access to; 
    PermitRootLogin no – disable login for root;
    PasswordAuthentication no – disable password login so that you can only log in using ssh keys`.

8. To install support libraries for the correct operation of a Python:
```bash
sudo apt-get install -y zsh tree redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python-pil python3-lxml libxslt1-dev python-libxml2 python-libxslt1 libffi-dev libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev
```
Brief information about libraries `
-y  - flag to prevent the installer from asking for confirmation of the package installation;
zsh – alternative to bash;
tree  – to view the folder structure;
redis-server  – storage;
nginx  – web server;
zlib1g-dev  – for correct operation of Python libraries
libbz2-dev  – 
libreadline-dev  – 
llvm  – 
libncurses5-dev  – 
libncursesw5-dev  – 
xz-utils  – 
tk-dev  – 
liblzma-dev  – 
python3-dev  –
python-pil  – 
python3-lxml  – to work correctly with xml inside Python
libxslt1-dev  – 
python-libxml2  – 
python-libxslt1  – 
libffi-dev  – 
libssl-dev  – to work with ssl
python-dev  – 
gnumeric  – 
libsqlite3-dev  – 
libpq-dev  – 
libxml2-dev  – 
libxslt1-dev  – 
libjpeg-dev  – 
libfreetype6-dev  – 
libcurl4-openssl-dev  – 
`.

## Step 2. Basic Python + Django template with nginx, gunicorn and systemd for Debian.

This is a basic server configuration template for implementing Python + Django web projects. The template implements the installation and configuration of nginx, gunicorn, and systemd.

The server configuration requires the following actions:
1. Create the "code" folder.
```bash
mkdir ~/code
```

2. Go to the "code" folder.
```bash
cd ~/code
```

3. Сopy git to the server
```bash
git clone https://github.com/lvg-alex/python-django-base-template.git
```
4. Check the "python-django-base-template" directory loaded on the server.
```bash
ls
```

5. Rename the "python-django-base-template" folder to "metrolog".
```bash
mv python-django-base-template metrolog
```

6. Go to the "metrolog" folder.
```bash
cd metrolog
```

7. View the contents of the "metrolog" folder.
```bash
ls
```

8. Сheck access rights to folder files
```bash
ls -la
```

9. Grant all access rights to directories and files:
```bash
sudo chmod 755 *
```
Rights values are represented in both alphabetic and numeric formats (`drwxr-xr-x (755)`).
Brief information: `d-indicates the file type, i.e. the directory;
rwx — all access rights for the owner;
r-x-read and execute permissions for the owner group;
r-x — the same rights for everyone else`.

10. To install, run the shell script:
```bash
./install.sh
```
Specify the Python interpreter (used to create a virtual environment):
    Python interpreter: '/home/www/.python/bin/python3.9'
Specify the IP address or domain name (specify the domain name or ip address of the hosting service):
    'XXX.XXX.XXX.XXX'
The template implements the installation and configuration of nginx, gunicorn, and systemd.

11. In the Django Configurator, set the database settings (`src/config/settings.py`).

12. Check the status of the gunicorn daemon:
```bash
sudo systemctl status gunicorn
```
The gunicorn logs are available in 'gunicorn/access. log' and `gunicorn/error. log'.

13. After changing the systemd configuration file, you need to re-read it and then restart the unit:
```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```
