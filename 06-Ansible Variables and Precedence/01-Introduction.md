
# Ansible variables and Precendence

## variables

In Ansible, variables are a key feature for parameterizing playbooks and roles, allowing for flexible and 
reusable automation scripts. Ansible variables can be defined in multiple places, and their precedence 
determines which value is used when there are conflicts. Here's a summary of Ansible variables and their 
precedence:

## Types of Variables

- Playbook Variables: Defined within playbooks.
- Inventory Variables: Defined in the inventory file or directory.
- Host Variables: Specific to a single host.
- Group Variables: Specific to a group of hosts.
- Role Variables: Defined within a role.
- Extra Variables: Passed at the command line using -e or --extra-vars.

## Variable Precedence

Ansible has a specific order of precedence for variables. Here’s the precedence order from lowest to highest 
(1 is the lowest, 17 is the highest):

- Role defaults: defaults/main.yml
- Inventory file or script group vars
- Inventory group_vars/all
- Playbook group_vars/all
- *Inventory group_vars/
- *Playbook group_vars/
- Inventory file or script host vars
- *Inventory host_vars/
- *Playbook host_vars/
- Host facts / cached set_facts
- Play vars
- Play vars_prompt
- Play vars_files
- Role vars: vars/main.yml
- Block vars: vars in blocks
- Task vars: vars in tasks
- Include vars: vars from include statements and roles
- Set_facts / registered vars: vars set by the set_fact module or by registering task outputs
- Role (and include_role) params
- Include params
- Extra vars: variables passed on the command line with -e

### Example
Consider a scenario where you have the same variable my_var defined in multiple places. The value used will 
be determined by the above precedence order.

### 1. Role defaults (roles/my_role/defaults/main.yml):
```
my_var: "default_value"
```
### 2. Inventory group_vars (inventory/group_vars/all.yml):
```
my_var: "group_var_value"
```
### 3. Playbook variable (playbook.yml):
```
- hosts: all
  vars:
    my_var: "playbook_value"
```
### 4. Extra vars (command line):
```
ansible-playbook playbook.yml -e my_var="extra_var_value"
```
Given these definitions, Ansible will use the value from the command line (extra_var_value) because it has 
the highest precedence.

## Managing Variables
To effectively manage variables, it’s essential to understand where they should be defined based on their 
intended scope and flexibility. Here are some tips:

- Use role defaults for providing default values that can be easily overridden.
- Define group and host variables in inventory files for variables specific to certain hosts or groups.
- Use playbook variables for values specific to a particular playbook.
- Leverage extra vars for temporary overrides, especially useful in CI/CD pipelines or during testing.

### Example Playbook
Here's an example playbook demonstrating variable usage:

```
---
- name: Example Playbook
  hosts: all
  vars:
    playbook_var: "playbook_value"
  tasks:
    - name: Print the value of my_var
      debug:
        msg: "my_var is {{ my_var }}"
    - name: Print the value of playbook_var
      debug:
        msg: "playbook_var is {{ playbook_var }}"
```
When running this playbook, you can override variables from the command line:

```
ansible-playbook playbook.yml -e my_var="command_line_value"
```
Understanding and effectively managing variable precedence allows for more flexible and powerful 
Ansible playbooks.







