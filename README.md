git_download_wordpress
=========

Ansible role that downloads and installs a chosen release of WordPress.

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the WordPress software. You can override those default variables if that is not the case.

Role Variables
--------------

To be filled in. This role is currently still a work in progress so I will fill these in once the first stable release is completed.

Dependencies
------------

None

Example Playbook
----------------

Copy and edit *defaults/main.yml* to your *vars/main.yml*

	- hosts: your_webserver
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.git_download_wordpress


or just pass the variables in the playbook


	- hosts: your_webserver 
	  vars:
		git_download_wordpress_tagged_release_version: "4.9.8"
		git_download_wordpress_db_user: "wordpressDbUser"
		git_download_wordpress_db_password: "some-really-secure-password"
		git_download_wordpress_mysql_root_password: "your-MySQL-root-password"
	  roles:
	    - stancel.git_download_wordpress

License
-------

GPLv3

Author Information
------------------

[Brad Stancel](https://github.com/stancel) 
