# python-django-base-template

It shows the sequence of actions that must be performed in order to install all the necessary packages on a clean Debian operating system and prepare the system for working with Django.

# Step 1. Debian Server Set Up for Django Instructions
Shows how to set up a clean Debian server for Python and Django projects. A secure SSH connection is implemented, packages are installed from Debian repositories and source code, and the Debian server is prepared to work with Django.

1. Launch cmd.exe () or powershell.exe.
```bash
cmd
```

## Create user, setup SSH
2. Configure a connection to a Debian VM using SSH. Create a new key using the ssh-keygen command. Execute the command:
```bash
ssh-keygen -t rsa -b 2048
```
After executing the command, specify the names of the files where the keys will be saved and enter the password for the private key. You will need to enter a keyword.
Keys are created in the directory C:\Users\<username>\ssh\. The public part of the key will be saved in a file named <key_name>.pub. The default name is id_rsa.
Save the generated key pair on the local machine.

3. Use the command line to connect to the VM:
```bash
C:\WINDOWS\system32>ssh <user name>@XXX.XXX.XXX.XXX
```
For example, for the user "www" and the ip address "127.0.0.1" will look like (`ssh www@127.0.0.1`).


# Step 2. Basic Python + Django template with nginx, gunicorn and systemd for Debian.

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
my python-django-base-template metrolog
```

6. Go to the "metrolog" folder.
```bash
cd metrolog
```

7. View the contents of the "metrolog" folder.
```bash
ls
```

8. To install, run the shell script:
```bash
./install.sh
```
Specify the Python interpreter (used to create a virtual environment):
    Python interpreter: '/home/www/.python/bin/python3.9'
Specify the IP address or domain name (specify the domain name or ip address of the hosting service):
    'XXX.XXX.XXX.XXX'
The template implements the installation and configuration of nginx, gunicorn, and systemd.

9. In the Django Configurator, set the database settings (`src/config/settings.py`).

10. Check the status of the gunicorn daemon:
```bash
sudo systemctl status gunicorn
```
The gunicorn logs are available in 'gunicorn/access. log' and `gunicorn/error. log'.

11. After changing the systemd configuration file, you need to re-read it and then restart the unit:
```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```
