git_download_wordpress
=========

Ansible role that downloads and installs a chosen release of WordPress.

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the WordPress software. You can override those default variables if that is not the case.

Role Variables
--------------

Is this a "new", "upgrade" or "restore" installation? "new" and "upgrade" installs install files from Git, "restore" skips any git deployments and expect a later role to restore files to the needed directory.
```
	git_download_wordpress_installation_type: "new"
```
Is this instance to be used for a "dev", "qa" or "prod" environment? Only "prod" environments will deploy any needed cron jobs or schedulers.
```
	git_download_wordpress_environment_type: "prod"
```

Choose the git tagged release that you would like to download and install. Comment this out if using a git branch instead.
```
	git_download_wordpress_tagged_release_version: "4.9.8"
```
The DB user to create when to be used by the application
```
	git_download_wordpress_db_user: "wordpressDbUser"
```
The password for the DB user being created
```
	git_download_wordpress_db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user.
```
	git_download_wordpress_mysql_root_password: "your MySQL root password"
```
Boolean as to whether to use standard Wordpress (default) or Bedrock WP (https://roots.io/bedrock/). The default is false.
```
	git_download_wordpress_use_bedrock: false
```
URL of the website. Not required or used unless using WP Bedrock
```
	git_download_wordpress_wp_home: "https://mywebsite.com"
```
Is this installation on a shared server? The default is false.
```
	git_download_wordpress_using_shared_server: false
```
The default git repo to use when downloading and installing the application
```
	git_download_wordpress_git_repo: "git@github.com:WordPress/WordPress.git"
```
The default git repo for downloading and installing Bedrock Wordpress
```
	git_download_wordpress_bedrock_git_repo: "git@github.com:roots/bedrock.git"
```
If you are using your own forked repo an want to use a branch instead of a tagged release then fill in a value and comment out the "tagged_release_version" variable. The default is an empty string "".
```
	git_download_wordpress_git_branch: ""
```
The database to create when setting up the application. The default is "wordpress"
```
	git_download_wordpress_db_name: "wordpress"
```
The default database character set / encoding that will be use. The default is "utf8mb4".
```
	git_download_wordpress_db_encoding: "utf8mb4"
```
The default database collation that will be use. The default is "utf8mb4_unicode_ci"
```
	git_download_wordpress_db_collation: "utf8mb4_unicode_ci"
```
The fqdn or IP address of where the application database will be connecting to. Default is 'localhost'.
```
	git_download_wordpress_db_host: "localhost"
```
WordPress Config Option - Disable All Updates. By default automatic updates are enabled in WordPress, set this value to true to disable all automatic updates. The default is false (i.e. allow WordPress to be updated in the app).
```
	git_download_wordpress_auto_update_disable: false
```
WordPress Config Option - Define Core Update Level
true  = Development, minor, and major updates are all enabled
false = Development, minor, and major updates are all disabled
minor = Minor updates are enabled, development, and major updates are disabled
For development sites, the default value of WP_AUTO_UPDATE_CORE is true. For other sites sites, the default value of WP_AUTO_UPDATE_CORE is minor.
```
	git_download_wordpress_core_update_level: 'minor'
```
The Document Root or file path where the files will be stored and served up by your webserver. The default path is `/var/www/html` and assumes you are running Nginx on Debian or Ubuntu.

First part => *git_download_wordpress_web_files_path:* is the root directory of your webserver

Second part =>  *git_download_wordpress_web_directory_for_application:* is the application directory inside the root directory

!Be aware of the starting / !
```
	git_download_wordpress_web_files_path: "/var/www"
	git_download_wordpress_web_directory_for_application: "/html"
```

The linux username used by your webserver. The default value is "www-data"
```
	git_download_wordpress_web_user: "www-data"
```
The linux group used by your webserver. The default value is "www-data".
```
	git_download_wordpress_web_group: "www-data"
```
Manage package with apt, you can disable the installation of package
```
	git_download_wordpress_manage_packages: true
```
Php.ini configurations flags, to allow or not the settings of these items, default is true, useful if your server is already setup with different values
```
	git_download_wordpress_configure_mysqli_allow_local_infile: true
	git_download_wordpress_configure_memory_limit: true
	git_download_wordpress_configure_post_max_size: true
	git_download_wordpress_configure_upload_max_filesize: true
	git_download_wordpress_configure_max_input_time: true
	git_download_wordpress_configure_max_execution_time: true
	git_download_wordpress_configure_php_timezone: true
```
Install composer or not, default true
```
	git_download_wordpress_install_composer: true
```


Dependencies
------------

NginX is the webserver this is currently written for since that is the PHP configuration this role updates (if you choose it to). `stancel.nginx_install` is what I use to install Nginx before this role is run. If using Bedrock WP, you'll need to have the WP CLI program installed prior to running this role. `sbaerlocher.wp-cli` is the one I use to install it prior to running this role.

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

