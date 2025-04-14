# INET4031 Puppet Configuration for LAMP Stack and User Management

# Program Description

This repository contains Puppet manifests designed to automate the process of configuring a LAMP stack and managing user accounts on a Linux system. Traditionally, setting up a LAMP server requires manually installing Apache, MySQL, and PHP, along with ensuring services are properly enabled and running. Likewise, managing users involves executing multiple commands, including adding users, setting passwords, and defining group assignments.
With Puppet, these tasks are streamlined by defining infrastructure as code (IaC). The Puppet manifests automate package installations, user account creation, and configuration enforcement, reducing errors and ensuring consistency across systems.

# Program User Operation
This section outlines the steps required to apply the Puppet manifests and verify their functionality.
User Management: server_users_groups.pp
This Puppet manifest automates the creation of system users and their group assignments. It ensures users are added with secure, hashed passwords instead of plaintext credentials.
Input Format
User definitions follow this format in the manifest:

user { 'username':
  ensure     => present,
  password   => '<hashed_password>',
  groups     => ['group01', 'group02'],
  managehome => true,
}

* username: The login name of the user.
* password: A securely hashed password generated using openssl passwd -6.
* groups: A list of groups the user should be assigned to. If no groups are required, omit this field.
* managehome: Ensures a home directory is created.

# Command Execution
Apply the manifest to create users:

sudo puppet apply server_users_groups.pp

Verify users:

cat /etc/passwd | grep user

Confirm group assignments:

cat /etc/group | grep group

# LAMP Stack: lamp_stack_server.pp
This Puppet manifest installs and configures a LAMP stack. It ensures Apache, PHP, and MariaDB are installed and running.
Command Execution

Apply the LAMP stack manifest:

sudo puppet apply lamp_stack_server.pp

Verify Apache is running:

sudo systemctl status apache2

Confirm PHP installation:

http://<server_ip>/phpinfo.php

Check MariaDB status:

sudo systemctl status mariadb
