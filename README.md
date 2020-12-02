# python-django-base-template
Basic Python + Django template with nginx, gunicorn and systemd for Debian.

This is a basic server configuration template for implementing Python + Django web projects. The template implements the installation and configuration of nginx, gunicorn, and systemd.

To install, run the shell script, specify the Python interpreter, and the domain name:
```bash
./install.sh
```

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
