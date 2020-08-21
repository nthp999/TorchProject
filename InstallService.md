# Install necessary services
#### 1. MySQL Server

**Step 1: Install MySQL**
- Download and install
`wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm`
`rpm -ivh mysql-community-release-el7-5.noarch.rpm`
`dnf install mysql-server`

- Start MySQL
      systemctl start mysqld

- Allows for improved security
      mysql_secure_installation
    - It will ask some question about secure privacy, which include password of database.

**Step 2: Create database and MySQL user for WordPress**
- Login mysql
      [root@localhost ~]# mysql -u root -p
      Enter password:

    - Password: the value have been enter in the previous step.

- Create database
      mysql> create database WordPress;
      Query OK, 1 row affected (0.00 sec)
    - *NOTE*: ';' is needed.

- Create user and password
      mysql> create user 'admin1'@'localhost' identified by 'password';
      Query OK, 0 rows affected (0.00 sec)

- Set privileges
      mysql> GRANT ALL PRIVILEGES ON wordpress.* TO 'admin1'@'localhost';
      Query OK, 0 rows affected (0.00 sec)

- Update change
      mysql> flush privileges;
      Query OK, 0 rows affected (0.00 sec)

- Exit
      mysql> exit
      Bye

#### 2. Apache

- Instal step by step
      sudo dnf update
      sudo dnf –y install httpd
  - Note:  "httpd" is the name for the Apache service in CentOS.  The –y option automatically answers yes to the confirmation prompt.

- Start and Manage Apache Web Server
      sudo systemctl start httpd
      sudo systemctl enable httpd
      sudo systemctl status httpd
      sudo systemctl reload httpd        //to apply the change

- Adjust Firewall for Apache
      sudo firewall-cmd --permanent --zone=public --add-service=http
      sudo firewall-cmd --permanent --zone=public --add-service=https
      sudo firewall-cmd --reload
      sudo firewall-cmd --list-all | grep services    //to check service
- Check
      curl localhost:80
