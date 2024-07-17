# Ansible Galaxy
Ansible Galaxy is a community hub for sharing Ansible roles and collections. It provides a platform where 
users can find, download, and share roles created by the Ansible community. Galaxy simplifies the reuse  
of automation code, helping users quickly set up and manage complex environments. Roles and collections  
on Galaxy include documentation and metadata, making it easier to understand their purpose and usage. 
The ansible-galaxy command-line tool allows users to install roles directly from Galaxy, facilitating  
the integration of community-contributed automation tasks into their own playbooks and workflows.

## Basic Commands and Their Usage with Ansible Galaxy for roles and collections.

### 1. Initialize a New Role

```
ansible-galaxy init <role_name>
```
### 2. Install Roles from Galaxy

```
ansible-galaxy install <role_name>
```
### 3. Install Roles from a requirements.yml File
- Example for requirements.yml File

```
- src: geerlingguy.apache
  version: 3.0.0
- src: git+https://github.com/username/repo.git
  version: master
  name: my_role
```

```
ansible-galaxy install -r requirements.yml
```
### 4. List Installed Roles

```
ansible-galaxy list
```
### 5. Remove an Installed Role

```
ansible-galaxy remove <role_name>
```
### 6. Create a Collection

```
ansible-galaxy collection init <namespace.collection_name>
```

### 7. Install Collections from Galaxy

```
ansible-galaxy collection install <collection_name>
```

### 8. Install Collections from a requirements.yml File

- Example for requirements.yml File

```
collections:
  - name: ansible.builtin
    version: 1.2.3
  - name: git+https://github.com/username/collection_repo.git
    type: git
    version: main
```

### 9. List Installed Collections

```
ansible-galaxy collection list
```

### 10. Remove an Installed Collection

```
ansible-galaxy collection uninstall ansible.builtin
```
These commands help you manage roles and collections effectively in Ansible Galaxy.

## Push your Ansible roles to Ansible Galaxy

1. Make sure your role is structured correctly. The basic structure should look like this:

```
my_role/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── tests/
│   ├── inventory
│   └── test.yml
└── vars/
    └── main.yml
```

2. Make sure ansible-galaxy CLI exists

```
ansible-galaxy --version
```

3. Push Your Role to GitHub

```
cd <role-name>
git init
git remote add origin <https://github.com/your_github_username/my_role.git>
git add .
git commit -m "Initial commit"
git push -u origin main
```

4. Import the Role to Ansible Galaxy

```
ansible-galaxy role import <your_github_username> <role-name>
```
