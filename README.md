# python-django-base-template
Basic Python + Django template with nginx, gunicorn and systemd for Debian.

This is a basic server configuration template for implementing Python + Django web projects. The template implements the installation and configuration of nginx, gunicorn, and systemd.

The server configuration requires the following actions:
1. Create the "code" folder.
```
mkdir ~/code
```

2. Go to the "code" folder.

To install, run the shell script:
```bash
./install.sh
```
Specify the Python interpreter, and the domain name:
''

In the Django Configurator, set the database settings (`src/config/settings.py`).

Check the status of the gunicorn daemon:
```bash
sudo systemctl status gunicorn
```

The gunicorn logs are available in 'gunicorn/access. log' and `gunicorn/error. log'.

After changing the systemd configuration file, you need to re-read it and then restart the unit:
```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```
