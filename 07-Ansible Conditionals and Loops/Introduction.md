# Ansible Conditionals and Loops

Ansible provides powerful features for handling conditionals and loops, which allow you to control the 
execution of tasks based on conditions and iterate over items. Here's an overview of how to use conditionals
and loops in Ansible.

## Conditionals

Conditionals in Ansible are used to execute tasks only when certain conditions are met. This is done using 
the when keyword.

### Basic Usage of when
```
- name: Install Apache on Debian-based systems
  apt:
    name: apache2
    state: present
  when: ansible_os_family == "Debian"
```

### Using Logical Operators
You can combine conditions using logical operators (and, or, not).

```
- name: Install Apache on Debian-based systems
  apt:
  name: apache2
  state: present
  when: ansible_os_family == "Debian" and ansible_distribution_version == "10"
```

### Checking Variable Values

```
- name: Restart Apache if configuration changed
  service:
  name: apache2
  state: restarted
  when: apache_config_changed
```

## Loops

Loops in Ansible allow you to repeat a task multiple times with different items. This is done using the loop
keyword.

### Basic Loop

```
- name: Install multiple packages
  apt:
  name: "{{ item }}"
  state: present
  loop:
    - apache2
    - nginx
    - mysql-server
```

### Loop with a Dictionary
You can loop over dictionaries using the with_dict keyword.

```
- name: Add multiple users
  user:
  name: "{{ item.key }}"
  state: present
  groups: "{{ item.value.groups }}"
  loop: "{{ users }}"
  vars:
  users:
  alice:
  groups: "admin"
  bob:
  groups: "users"
```

### Loop with a Range
You can use a range to loop over a sequence of numbers.

```
- name: Create multiple users
  user:
    name: "user{{ item }}"
    state: present
  loop: "{{ range(1, 5) }}"
```

### Loop with Subelements
You can loop over nested data structures using subelements.

```
- name: Install application and its dependencies
  yum:
    name: "{{ item.1 }}"
    state: present
  loop: "{{ applications | subelements('dependencies') }}"
  vars:
    applications:
      - name: app1
        dependencies:
          - dep1
          - dep2
      - name: app2
        dependencies:
          - dep3
          - dep4
```

### Combining Loops and Conditionals
You can combine loops and conditionals to control the execution of tasks more precisely.

```
- name: Install packages on Debian-based systems
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - apache2
    - nginx
    - mysql-server
  when: ansible_os_family == "Debian"
```

## Example Playbook
Here’s an example playbook that demonstrates the use of conditionals and loops:

```
---
- name: Ansible Conditionals and Loops Example
  hosts: all
  vars:
    packages:
      - apache2
      - nginx
      - mysql-server
    users:
      - name: alice
        groups: admin
      - name: bob
        groups: users
  tasks:
    - name: Install packages on Debian-based systems
      apt:
        name: "{{ item }}"
        state: present
      loop: "{{ packages }}"
      when: ansible_os_family == "Debian"

    - name: Add multiple users
      user:
        name: "{{ item.name }}"
        state: present
        groups: "{{ item.groups }}"
      loop: "{{ users }}"
```

In above playbook:

- Packages are installed on Debian-based systems only.
- Multiple users are added based on the provided list.

By using conditionals and loops effectively, you can make your Ansible playbooks more dynamic and powerful,
allowing for complex automation scenarios.




















