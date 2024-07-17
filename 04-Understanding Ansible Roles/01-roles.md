# Ansible Roles

An Ansible role is a reusable, self-contained unit of automation that is used to 
organize and manage tasks, variables, files, templates, and handlers in a structured way. 

Roles help to encapsulate and modularize the logic and configuration needed to manage 
a particular system or application component. 

This modular approach promotes reusability, maintainability, and consistency across different 
playbooks and environments.

## Key Components of an Ansible Role

### Tasks
The main list of actions that the role performs.

### Handlers
Tasks that are triggered by changes in other tasks, typically used for actions like restarting services.

### Files
Static files that need to be transferred to managed hosts.

### Templates
Jinja2 templates that can be rendered and transferred to managed hosts.

### Vars
Variables that are used within the role.

### Defaults
Default variables for the role, which can be overridden.

### Meta
Metadata about the role, including dependencies on other roles.

### Library
Custom modules or plugins used within the role.

### Module_defaults
Default module parameters for the role.

### Lookup_plugins
Custom lookup plugins for the role.

## Directory Structure of an Ansible Role

An Ansible role follows a specific directory structure:

```
roles/
  └── <role_name>/
      ├── tasks/
      │   └── main.yml
      ├── handlers/
      │   └── main.yml
      ├── files/
      ├── templates/
      ├── vars/
      │   └── main.yml
      ├── defaults/
      │   └── main.yml
      ├── meta/
      │   └── main.yml
      └── README.md

```

Here's a brief description of each directory and file:

- tasks/main.yml: Contains the main list of tasks to be executed by the role.

- handlers/main.yml: Defines handlers that can be triggered by tasks.

- files/: Stores files that can be deployed to the managed hosts.

- templates/: Contains Jinja2 templates that can be dynamically filled and deployed.

- vars/main.yml: Defines variables specific to the role.

- defaults/main.yml: Sets default variables for the role, which can be overridden.

- meta/main.yml: Provides metadata about the role, such as its dependencies.

- README.md: Documentation for the role.

## Why Use Ansible Roles?

### Modularity
Roles allow you to break down complex playbooks into smaller, reusable components. 
Each role handles a specific part of the configuration or setup.

### Reusability
Once created, roles can be reused across different playbooks and projects. This saves time 
and effort in writing redundant code.

### Maintainability
By organizing related tasks into roles, it becomes easier to manage and maintain the code. 
Changes can be made in one place and applied consistently wherever the role is used.

### Readability
Roles make playbooks cleaner and easier to read by abstracting away the details into logically
named roles.

### Collaboration
Roles facilitate collaboration among team members by allowing them to work on different parts
of the infrastructure independently.

### Consistency
Using roles ensures that the same setup and configuration procedures are applied uniformly across
multiple environments, reducing the risk of configuration drift.

## Creating a Role

### To create a new role, you can use the ansible-galaxy command:

```
ansible-galaxy init <role_name>
```
This command creates a new directory structure for the role.

## Using Roles in a Playbook
Once a role is created, you can use it in your playbooks. Here’s an example playbook that uses a role:

```
---
- name: Apply the webserver role
  hosts: webservers
  roles:
    - webserver
```
In this example, the webserver role will be applied to all hosts in the webservers group.

## Example Role Structure
Let's create a simple role named webserver to install and configure an Apache web server.

### Directory structure:

```
roles/
  └── webserver/
      ├── tasks/
      │   └── main.yml
      ├── handlers/
      │   └── main.yml
      ├── files/
      │   └── index.html
      ├── templates/
      │   └── httpd.conf.j2
      ├── vars/
      │   └── main.yml
      ├── defaults/
      │   └── main.yml
      ├── meta/
      │   └── main.yml
      └── README.md

```

### tasks/main.yml:

```
---
- name: Install Apache
  apt:
    name: apache2
    state: present
  notify:
    - Start Apache

- name: Deploy index.html
  copy:
    src: index.html
    dest: /var/www/html/index.html
```

### handlers/main.yml:

```
---
- name: Start Apache
  service:
    name: apache2
    state: started
    enabled: yes
```

### files/index.html:

```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Apache!</title>
</head>
<body>
    <h1>It works!</h1>
</body>
</html>
```

### templates/httpd.conf.j2:

```
# Apache configuration template
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost
```
vars/main.yml and defaults/main.yml can be used to define variables for the role, such as configuration parameters or file paths.

### meta/main.yml:

```
---
dependencies: []
```

## Running the Playbook
To run the playbook that uses this role, you would use the ansible-playbook command:

```
ansible-playbook -i inventory playbook.yml
```

This approach allows you to create modular and reusable components, making it easier to manage and scale your infrastructure automation with Ansible.
























































