# Examination 8 - MariaDB configuration

MariaDB and MySQL have the same origin (MariaDB is a fork of MySQL, because of... Oracle...
it's a long story.) They both work the same way, which makes it possible to use Ansible
collections that handle `mysql` to work with `mariadb`.

To be able to manage MariaDB/MySQL through the `community.mysql` collection, you also
need to make sure the requirements for the collections are installed on the database VM.

See https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_db_module.html#ansible-collections-community-mysql-mysql-db-module-requirements

HINT: In AlmaLinux, the correct package to install on the VM host is called `python3-PyMySQL`.

# QUESTION A

Copy the playbook from examination 7 to `08-mariadb-config.yml`.

Use the `community.mysql` module in this playbook so that it also creates a database instance
called `webappdb` and a database user called `webappuser`.

Make the `webappuser` have the password "secretpassword" to access the database.

HINT: The `community.mysql` collection modules has many different ways to authenticate
users to the MariaDB/MySQL instance. Since we've just installed `mariadb` without setting
any root password, or securing the server in other ways, we can use the UNIX socket
to authenticate as root:

* The socket is located in `/var/lib/mysql/mysql.sock`
* Since we're authenticating through a socket, we should ignore the requirement for a `~/.my.cnf` file.
* For simplicity's sake, let's grant `ALL` privileges on `webapp.*` to `webappuser`

Svar:
För att skapa databasen och användaren i MariaDB med Ansible:

Jag installerade python3-PyMySQL på databasservern, eftersom det krävs för att community.mysql ska fungera.

Jag använde community.mysql.mysql_db för att skapa databasen webappdb.

Jag använde community.mysql.mysql_user för att skapa användaren webappuser med lösenord secretpassword.

Jag gav användaren ALL-rättigheter på webapp.* enligt instruktionen.

Jag använde login_unix_socket: /var/lib/mysql/mysql.sock och check_implicit_admin: true för att logga in som root utan ~/.my.cnf.

Allt kördes automatiskt via en Ansible-playbook.

# Documentation and Examples
https://docs.ansible.com/ansible/latest/collections/community/mysql/index.html
