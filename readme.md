# установка ansimble
 
```
sudo apt install -y sshpass;
sudo apt install ansible-core;
```

ansible-playbook -i SERVER_IP, build-web-server.yml -u root --ask-pass

ansible-playbook -i inventory.ini get-backup-front.yml

ansible-playbook -i inventory.ini get-dump.yml

# создать контейнер
docker run -d \
  --name mariadb-10.3 \
  -e MARIADB_ROOT_PASSWORD=my-secret-pw \
  -p 3306:3306 \
  -v ./mariadb-data:/var/lib/mysql \
  mariadb:10.3.39


<!-- docker exec -it mariadb-10.3 mysql -u root -pmy-secret-pw -e "SELECT VERSION();" -->

# create db
docker exec -it mariadb-10.3 mysql -u root -pmy-secret-pw -e "create database crm_mif_dev"


# dump
cat crm-mif-dev_backup.sql | docker exec -i mariadb-10.3 mysql -u root -p'my-secret-pw' crm_mif_dev

# зайти в консоль 
docker exec -it mariadb-10.3 mysql -u root -p