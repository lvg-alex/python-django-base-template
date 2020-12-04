# python-django-base-template

It shows the sequence of actions that must be performed in order to install all the necessary packages on a clean Debian operating system and prepare the system for working with Django.

## Step 1. Configure a connection to a Debian VM using SSH

1. Launch cmd.exe or powershell.exe.
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


## Step 2. Debian Server Set Up for Django Instructions
Shows how to set up a clean Debian server for Python and Django projects. A secure SSH connection is implemented, packages are installed from Debian repositories and source code, and the Debian server is prepared to work with Django.

1. Update repositories and install some initial needed packages:
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

2. Configure SSH so that the user <user name> can connect via SSH.
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

3. To install support libraries for the correct operation of a Python:
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

4. Install [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh):
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
oh-my-zsh – a convenient set of plugins and configurations over zsh.
Set zsh as the default shell:
```bash
chsh -s $(which zsh)
```
Show where zsh is currently located
```bash
which zsh
```

5. Install python 3.9
Build from source python 3.9, install with prefix to `~/.python` folder.
5.1. Download sources
```bash
wget https://www.python.org/ftp/python/3.9.0/Python-3.9.0.tgz
```
5.2. Unzip the source code
```bash
tar xvf Python-3.9.*
```
5.3. Go to directory
```bash
cd Python-3.9.0
```
5.4. Create a folder where we will install all Python dependencies
```bash
sudo mkdir ~/.python
```
5.5. Сonfigure the installer
During installation, configure the installer so that it installs all dependencies in a specific directory. This allows you to remove dependencies from a single directory, rather than searching for them on disk.
```bash
./configure --enable-optimizations --prefix=/home/www/.python
```
Brief information about libraries `-- prefix=/home/www/.python-specifies the directory where everything is installed`.

5.6. Build code from source
```bash
make -j4
```
5.7. Install the assembled product
```bash
sudo make altinstall
```
5.8. Update pip
```bash
sudo /home/www/.python/bin/python3.9 -m pip install -U pip
```
5.9. Delete the file with the archive, and source codes
```bash
cd ..
sudo rm -rf Python-3.9.0.tgz Python-3.9.0
```
5.10. To check if all files were installed
```bash
ls -la
pwd
```

6. Сhange the color scheme in VIM

In Vim, you can use different color schemes. You can configure the scheme by changing the configuration file. For a list of existing color schemes, see the directory ` '/usr/share/vim/vim_version/colors`.
To change the scheme to `desert`, run the command `: colorscheme desert` in vim (press ESC, enter the command, and press ENTER).
Changes will only apply during the current editing session.

To make the settings always work you need to configure the configuration file:
```bash
cd
ls -la
vim .vimrc
```
Add to the file
```bash
    syntax on
    colorscheme desert
```

7. For convenience of further configuration, create a session in the terminal multiplexer
```bash
tmux new-session -s dev
```
Add a panel (split the screen horizontally): `Ctrl+b    "`
Switch between panels `Ctrl+b + arrow`. The arrow indicates the direction in which to switch the panel.
Log out of the session `Ctrl+b + d`.
Connect to a terminal multiplexer session named " dev": `tmux attach-session -t dev`.

8. Configure a non-standard tmux configuration
```bash
cd
git clone https://github.com/gpakosz/.tmux.git
ln -s -f .tmux/.tmux.conf
cp .tmux/.tmux.conf.local .
```
Save the changes, press `Ctrl+b :`, then to restart tmux run the command:
```bash
source ~/. tmux. conf
```
You can also use `Ctrl+b :` and then `r` to apply the configuration parameters.
The interface will change.

## Step 3. Basic Python + Django template with nginx, gunicorn and systemd for Debian.

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

11. Check the status of the gunicorn daemon:
```bash
sudo systemctl status gunicorn
```
The gunicorn logs are available in 'gunicorn/access. log' and `gunicorn/error. log`.

12. After changing the systemd configuration file, you need to re-read it and then restart the unit:
```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```

13. Configure the display of the design on the nginx server.
Go to the project directory
```bash
cd code/metrolog/
```
Activate the created environment
```bash
. env/bin/activate
```
Find the root directory of the Django module:
```bash
python -c "
import sys
sys.path = sys.path[1:]
import django
print(django.__path__)"
```
Example of the command execution result:
`['/home/www/code/metrolog/env/lib/python3.9/site-packages/django']`

Static files for the admin panel are located in contrib/admin/static/admin/:
```bash
ls -l /home/www/code/metrolog/env/lib/python3.9/site-packages/django/contrib/admin/static/admin/
```
Example of the command execution result:
`total 16
drwxr-xr-x 3 www www 4096 Dec  2 21:44 css
drwxr-xr-x 2 www www 4096 Dec  2 21:44 fonts
drwxr-xr-x 3 www www 4096 Dec  2 21:44 img
drwxr-xr-x 4 www www 4096 Dec  2 21:44 js`

Create an alias for /static/ in the NGINX configuration:
```bash
vim nginx/site.conf
```

Delete from the `site.conf`file:
```site.conf
    location /static/ {
        root /home/www/code/metrolog/static;
    }
```

There are alternative options:
- the first (is preferred)
Recursively copying the `/home/www/code/metrolog/env/lib/python3.9/site-packages/django/contrib/admin/static/` directory from the current location to the new `/home/www/code/metrolog/static` directory:
```bash
cp -r /home/www/code/metrolog/env/lib/python3.9/site-packages/django/contrib/admin/static/ /home/www/code/metrolog/static
```
Add to the file `site.conf`:
```site.conf
    location /static/ {
        alias /home/www/code/metrolog/static/;
        expires modified +1w;
    }
```   
    
- the second:
Add to the file `site.conf`:
```site.conf
    location /static/ {
        alias /home/www/code/metrolog/env/lib/python3.9/site-packages/django/contrib/admin/static/;
        expires modified +1w;
    }
```

Check the NGINX configuration:
```bash
sudo nginx -t
```
Example of the command execution result (on success): 
    `nginx: the configuration file /etc/nginx/nginx.conf syntax is ok`
    `nginx: configuration file /etc/nginx/nginx.conf test is successful`

Restart the server:
```bash
sudo service nginx restart
```

## Step 4. Install and configure PostgreSQL
To configure a PostgreSQL + Python + Django bundle, follow these steps:

1. Сonfigure locale
```bash
sudo localedef ru_RU.UTF-8 -i ru_RU -fUTF-8 ; \
export LANGUAGE=ru_RU.UTF-8 ; \
export LANG=ru_RU.UTF-8 ; \
export LC_ALL=ru_RU.UTF-8 ; \
sudo locale-gen ru_RU.UTF-8 ; \
sudo dpkg-reconfigure locales
```
Add locales to `/etc/profile`:
```bash
sudo vim /etc/profile
    export LANGUAGE=ru_RU.UTF-8
    export LANG=ru_RU.UTF-8
    export LC_ALL=ru_RU.UTF-8
```

2. Install and base configure PostgreSQL (version 11)
```bash
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - ; \
RELEASE=$(lsb_release -cs) ; \
echo "deb http://apt.postgresql.org/pub/repos/apt/ ${RELEASE}"-pgdg main | sudo tee  /etc/apt/sources.list.d/pgdg.list ; \
sudo apt update ; \
sudo apt -y install postgresql-11
```

3. Change `postges` password, create clear database named `metrolog_db`:
```bash
sudo passwd postgres
```
Example of the command execution result (on success): 
    `New password:`
    `Retype new password:`
    `passwd: password updated successfully`
    
4. Log in to the DBMS as a user
```bash
su postgres
```
Example of the command execution result (on success): 
    `Password:`
    `postgres@python-dev:/home/www/code/metrolog$`

5. Export a directory
```bash
export PATH=$PATH:/usr/lib/postgresql/11/bin
```

6. Create metrolog_db database
```bash
createdb --encoding UNICODE metrolog_db --username postgres
exit
```

7. Create `www_dbms` db user and grand privileges to him:
```bash
sudo -u postgres psql
```
- Сreate a user with a password using the command:
```postgres
    create user www_dbms with password '<your password>';
```
Example of the command execution result (on success): 
`   psql (11.10 (Debian 11.10-1.pgdg100+1))`\
`   Type "help" for help.`\
`    `\
`   postgres=# create user www_dbms with password '1q2w*****7';`\
`   CREATE ROLE`

- Allow the user to create a database:
```postgres
ALTER USER www_dbms CREATEDB;
```
Example of the command execution result (on success):  
`    postgres=# ALTER USER www_dbms CREATEDB;`\
`   ALTER ROLE`

- Grant privileges to a newly created database
```postgres
grant all privileges on database metrolog_db to www_dbms;
```
Example of the command execution result (on success):  
`   postgres=# grant all privileges on database metrolog_db to www_dbms;`\
`   GRANT`

- Grant access to the user
```postgres
\c metrolog_db
```
Example of the command execution result (on success):  
`   postgres=# \c metrolog_db`\
`   You are now connected to database "metrolog_db" as user "postgres".`\
`   metrolog_db=# `

- Execute the command:
```postgres
GRANT ALL ON ALL TABLES IN SCHEMA public to www_dbms;
GRANT ALL ON ALL SEQUENCES IN SCHEMA public to www_dbms;
GRANT ALL ON ALL FUNCTIONS IN SCHEMA public to www_dbms;
CREATE EXTENSION pg_trgm;
ALTER EXTENSION pg_trgm SET SCHEMA public;
```
Example of the command execution result (on success):  
`   metrolog_db=# GRANT ALL ON ALL TABLES IN SCHEMA public to www_dbms;`\
`   GRANT`\
`   metrolog_db=# GRANT ALL ON ALL SEQUENCES IN SCHEMA public to www_dbms;`\
`   GRANT`\
`    metrolog_db=# GRANT ALL ON ALL FUNCTIONS IN SCHEMA public to www_dbms;`\
`   GRANT`\
`   metrolog_db=# CREATE EXTENSION pg_trgm;`\
`    CREATE EXTENSION`\
`   metrolog_db=# ALTER EXTENSION pg_trgm SET SCHEMA public;`\
`   ALTER EXTENSION`\
`   metrolog_db=#`

- Enable extensions for programmatic search in the string column:
```postgres
UPDATE pg_opclass SET opcdefault = true WHERE opcname='gin_trgm_ops';
```
Example of the command execution result (on success):  
`   metrolog_db=# UPDATE pg_opclass SET opcdefault = true WHERE opcname='gin_trgm_ops';`\
`   UPDATE 1`\
`   metrolog_db=#`

- exit
```postgres
\q
```

8. Check the connection.
Create a `~/.pgpass` file with the database username and password for quick connection:
```bash
vim ~/.pgpass
    localhost:5432:metrolog_db:www_dbms:<your password>
```
Close the Vim and save result: `ESC -> : -> wq -> ENTER`

Change access rights to the file:
```bash
vim ~/.pgpass
chmod 600 ~/.pgpass
```
- Now you can log in without a password for this database!
```bash
psql -h localhost -U www_dbms metrolog_db
```
Example of the command execution result (on success):  
`   ➜  ~ psql -h localhost -U www_dbms metrolog_db`\
`    Пароль пользователя www_dbms:`\
`   psql (11.10 (Debian 11.10-1.pgdg100+1))`\
`   SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)`\
`   Введите "help", чтобы получить справку.`\
`   `\
`   metrolog_db=>`
- exit
```postgres
\q
```

9. Run SQL dump, if you have
```bash
psql -h localhost metrolog_db www_dbms  < dump.sql
```

10. In the Django Configurator, set the database settings (`src/config/settings.py`).
```bash
vim src/config/settings.py
```
Example of the command execution result (on success):  

# Database
`...`\
`# https://docs.djangoproject.com/en/2.2/ref/settings/#databases`\
`   DATABASES = {`\
`       'default': {`\
`           'ENGINE': 'django.db.backends.postgresql_psycopg2',`\
`           'NAME': 'metrolog_db',`\
`           'USER': 'www_dbms',`\
`           'PASSWORD': '1q2w!Q@W77',`\
`           'HOST': 'localhost',`\
`           'PORT': '',`\
`       }`\
`   }`\
`...`\

11. Create an SQL dump:
- basic command on the local server (`the "-W " option will require you to enter a password`)
```bash
pg_dump -U www_dbms -W metrolog_db > /tmp/metrolog_db.dump
```
- command on remote server
```bash
pg_dump -h 10.0.0.10 metrolog_db > /tmp/metrolog_db.dump
```

12. Data compression:
```bash
pg_dump metrolog_db | gzip > metrolog_db.dump.gz
```

13. Script for automatic backup:
To run a scheduled backup, save the script to a file, for example, /scripts/postgresql_dump.sh.
```postgresql_dump.sh
#!/bin/sh
PATH=/etc:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin

PGPASSWORD=password
export PGPASSWORD
pathB=/backup
dbUser=www_dbms
database=metrolog_db

find $pathB \( -name "*-1[^5].*" -o -name "*-[023]?.*" \) -ctime +61 -delete
pg_dump -U $dbUser $database | gzip > $pathB/pgsql_$(date "+%Y-%m-%d").sql.gz

unset PGPASSWORD
```
`password` - password for connecting to postgresql;
`/backup` - the folder where backups will be stored;
`www_dbms` — name of the account to connect to the DBMS.
The script will delete all backups older than 61 days, but will leave the 15th as a long archive. After that, the pg_dump utility will be used to connect and reserve the `metrolog_db` database. The password is exported to the system variable at the time of the task execution.

- Create a task in the scheduler:
```bash
3 0 * * * /scripts/postgresql_dump.sh
```
The script will run every day at 03:00.
