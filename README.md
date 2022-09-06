# Setup MySQL 8.0

## Install MySQL

`sudo apt install mysql-server`

Start using systemctl

`sudo systemctl start mysql.service`

Verify started successfully:

`sudo systemctl status mysql`

## Configure MySQL

Change the authentication method to mysql_native_password using password as [admin@123]:

```
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'admin@123';
exit
```

Enable remote access
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`

Comment out these settings

```
# bind-address          = 127.0.0.1
# mysqlx-bind-address   = 127.0.0.1
```

Restart MySQL
`sudo systemctl restart mysql`

Change password validation policy

```
mysql -u root -padmin@123
SHOW VARIABLES LIKE 'validate_password%';
SET GLOBAL validate_password.policy=LOW;
exit
```

## Create user `admin`

Create user for remote access

```
mysql -u root -padmin@123
CREATE USER 'admin'@'%' IDENTIFIED BY 'admin@123';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
```
