# Ansible Adhoc Commands

## Understanding Adhoc Commands

Ad-hoc commands in Ansible are commands that you can run on remote hosts without having to write a playbook. 
They are useful for tasks that you want to perform quickly and don't require complex orchestration or 
conditions. Ad-hoc commands are typically run from the command line using the ansible command followed by 
various options and arguments.

### Syntax

```
ansible [pattern] -m [module] -a "[arguments]" -i [inventory]
```

### Explanation
pattern: Specifies which hosts to target.
- -m [module]: Indicates the module to run (e.g., ping, shell, copy).
- -a "[arguments]": Provides arguments required by the module.
- -i [inventory]: Specifies the inventory file.

### Common Adhoc Commands

- Adhoc commands are useful for quick system management tasks.

1. Rebooting a Host
- Reboot all hosts:

```
ansible all -m reboot -i inventory.ini
```

2. Checking Disk Usage
- Check disk usage:

```
ansible all -m shell -a 'df -h' -i inventory.ini
```

3. Managing Services

- Starting a Service
- Start httpd service:

```
ansible all -m service -a 'name=httpd state=started' -i inventory.ini
```

4. Stopping a Service
- Stop httpd service:

```
ansible all -m service -a 'name=httpd state=stopped' -i inventory.ini
```

5. Installing Packages
- Install vim package:

```
ansible all -m yum -a 'name=vim state=present' -i inventory.ini
```

6. Copying Files
- Copy a file from local to remote:

```
ansible all -m copy -a 'src=/path/to/local/file dest=/path/to/remote/file' -i inventory.ini
```

7. User Management
- Create a new user:

```
ansible all -m user -a 'name=ansible state=present' -i inventory.ini
```

8. Checking Uptime
- Check uptime:

```
ansible all -m command -a 'uptime' -i inventory.ini
```

These examples showcase the flexibility and power of Ansible ad-hoc commands for quickly performing system
management tasks across multiple hosts defined in your inventory. They are particularly useful for tasks 
that do not require complex automation or when you need to perform quick checks or operations.
