# python-django-base-template

# I Debian Server Set Up for Django Inctruction
Shows how to set up a clean Debian server for Python and Django projects. A secure SSH connection is implemented, packages are installed from Debian repositories and source code, and the Debian server is prepared to work with Django.

// TODO

# II Basic Python + Django template with nginx, gunicorn and systemd for Debian.

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
