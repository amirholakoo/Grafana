# Grafana Installation Guide
 
### Installation

sudo apt-get install -y software-properties-common

sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

sudo apt-get update

sudo apt-get install grafana

sudo systemctl start grafana-server

sudo systemctl enable grafana-server

### Config MySQL

sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

bind-address            = 0.0.0.0


### Access/Permission

sudo mysql -u root -p

CREATE USER 'grafanaReader' IDENTIFIED BY 'pi';

GRANT SELECT ON *.* TO 'grafanaReader';

SELECT user, host FROM mysql.user WHERE user = 'grafanareader';

GRANT ALL PRIVILEGES ON *.* TO 'grafanareader'@'192.168.1.101' IDENTIFIED BY 'pi';

FLUSH PRIVILEGES;

exit;

sudo service mysql restart

### Access Grafana

Open a web browser and go to http://your-raspberry-pi-ip:3000/. The default login is admin for both the user and password.
