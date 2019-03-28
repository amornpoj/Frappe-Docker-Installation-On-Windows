# Clone Repository
```
- git clone --branch windows https://github.com/sopanawit/frappe_docker.git
- cd .\frappe_docker\
- docker-compose up -d
```


# Set MariaDB
```
- docker exec -it mariadb bash
- apt-get -y update
- apt-get -y install vim
- cd /etc/mysql
- vim my.cnf
```
Add the following lines under the [mysqld] line.
```
innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
```
Also, add the following line under the [mysql] line.
```
default-character-set = utf8mb4
```
Restart docker compose.
```
docker-compose restart
```
 
 
# Install Frappe
```
- docker exec -it frappe bash
- mv Procfile_docker Procfile
- mv sites/common_site_config_docker.json sites/common_site_config.json
- bench set-mariadb-host mariadb
- cd /home/frappe
- bench init frappe-bench --ignore-exist --skip-redis-config-generation --frappe-path=[URL Cappuccino] --frappe-branch=ktb-dorm
```



# Create a new Frappe site & install dorm app
```
- docker exec -it frappe bash
- bench build
- bench update --requirements
- bench new-site frappe.local
- bench get-app roommage [URL Roommage Web App] --branch=develop
- bench --site frappe.local install-app roommage
```
You can start the application immediately to check if the application installed successfully.
```
bench start
```
