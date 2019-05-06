# Prerequsite
```
1. OS : Windows / MacOS
2. Docker Toolbox
3. Docker Compose
4. Git
5. Visual Studio Code
6. Remote Workspace Extension for Visual Studio Code
```


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
exit
docker-compose restart
```
 
 
# Install Frappe
```
- docker exec -it frappe bash
- mv Procfile_docker Procfile
- mv sites/common_site_config_docker.json sites/common_site_config.json
- bench set-mariadb-host mariadb
- cd /home/frappe
- bench init frappe-bench --ignore-exist --skip-redis-config-generation 
  frappe-path=[URL Cappuccino] --frappe-branch=[Branch]
```


# Create a new site
```
- docker exec -it frappe bash
- bench build
- bench update --requirements
- bench new-site [Site Name]
```


# Install Dorm app
```
- bench get-app roommage [URL Dormitory Web App] --branch=develop
- bench --site frappe.local install-app roommage
```
You can start the application immediately to check 
if the application installed successfully.
```
bench start
```


# Develop frappe application using Git
```
$ cd apps/<app_name>
$ git remote -v
$ git remote remove upstream
$ git remote add origin <repository_url>
$ git remote -v
$ git fetch origin <branch_name> && git pull
$ git checkout <branch_name>
$ git status
```


# Development using Remote Workspace
Password that defined in `frappe-bench.code-workspace` is __1q2w3e4r__ 
but if you want to use you own password, workspace file must be fixed.
```
C:\Users\<user>\<path>\frappe_docker> docker exec -it frappe bash
frappe:~/frappe-bench$ sudo su
frappe:~/frappe-bench$ passwd frappe
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```


## Open workspace file with Visual Studio Code
```
File > Open Workspace > frappe-bench.code-workspace
```
