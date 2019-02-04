# Clone Frappe-Docker
- git clone https://github.com/frappe/frappe_docker.git
- cd .\frappe_docker\
- docker-compose up -d
 
 
# Set Root Frappe Bash
- docker exec -itu root frappe bash
- cd /home/frappe/ && chown -R frappe:frappe ./*
- exit
 
 
# Set Frappe Bash & Install Erpnext
- docker exec -it frappe bash
- cd /home/frappe/ && bench init erpnext
- sudo apt update
- sudo pip install -e bench-repo
- sudo npm install -g yarn
- exit


# Config MariaDB (Permission)
- docker exec -it mariadb bash
- apt-get -y update
- apt-get -y install vim
- cd /etc/mysql/
- chmod -R 0444 ./conf.d/*
- exit
- docker-compose restart


# Copy File From Frappe-Bench
- docker exec -it frappe bash
- mv Procfile_docker Procfile && mv sites/common_site_config_docker.json sites/common_site_config.json && bench set-mariadb-host mariadb
- cp Procfile ../erpnext/
- cp sites/common_site_config.json ../erpnext/sites/
- cd /home/frappe/ && sudo chmod -R 777 erpnext
- exit
 
 
# Create New Site  &&  Install ErpNext App
- docker exec -it frappe bash
- cd /home/frappe/erpnext
- bench new-site site1.local
- bench get-app erpnext https://github.com/frappe/erpnext
- bench --site site1.local install-app erpnext
- cd /home/frappe/
- sudo chown -R frappe:frappe ~/.config
- cd /home/frappe/erpnext
- bench update
- bench update --patch
- bench start
