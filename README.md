# Grafana Installation Guide
 
### Installation

`sudo apt-get install -y software-properties-common`

`sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"`

`wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -`

`sudo apt-get update`

`sudo apt-get install grafana`

`sudo systemctl enable grafana-server`

`sudo systemctl start grafana-server`

### Config MySQL

`sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf`

bind-address            = 0.0.0.0


### Access/Permission

`sudo mysql -u root -p`

`CREATE USER 'grafana'@'%' IDENTIFIED BY 'pi';`

`GRANT SELECT ON *.* TO 'grafana';`

`grant usage on *.* to 'grafana'@'%' IDENTIFIED BY 'pi';`

`GRANT ALL PRIVILEGES ON *.* TO 'grafana'@'%';`

`SELECT user, host FROM mysql.user WHERE user = 'grafana';`

`GRANT ALL PRIVILEGES ON *.* TO 'grafana'@'192.168.1.101' IDENTIFIED BY 'pi';`

`FLUSH PRIVILEGES;`

`exit;`

`sudo service mysql restart`

### Access Grafana

Open a web browser and go to http://your-raspberry-pi-ip:3000/. The default login is admin for both the user and password.

### SQLite Plugin:

`sudo systemctl stop grafana-server`

`sudo chmod 777 /var/lib/grafana`

Either:

Find the latest version here: 

https://github.com/fr-ser/grafana-sqlite-datasource/releases

Check Version BELOW:
`grafana-cli --pluginUrl https://github.com/fr-ser/grafana-sqlite-datasource/releases/download/v3.5.0/frser-sqlite-datasource-3.5.0.zip plugins install frser-sqlite-datasource`
OR
`grafana-cli plugins install frser-sqlite-datasource`

### POSTgre SQL

Install PostgreSQL: Install PostgreSQL on your system. You can download it from the official PostgreSQL website.

Create a Database: Once PostgreSQL is installed, create a database for your application. You can use the `psql` command-line tool to create a database:

`createdb mydatabase`

Modify Django Settings: In your Django project's settings.py file, update the DATABASES setting to use PostgreSQL:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'myusername',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

Install psycopg2: Install the psycopg2 library, which is a PostgreSQL adapter for Python. You can install it using pip:

`pip install psycopg2-binary`

Migrate Database: Run Django's migrate command to create the necessary database tables:

`python manage.py migrate`


