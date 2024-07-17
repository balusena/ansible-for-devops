# Error Handling in Ansible

Error handling in Ansible allows you to manage and control the behavior of your playbooks when tasks fail. 
This is essential for creating robust automation scripts that can handle unexpected situations gracefully. 
Here are the key concepts and techniques for error handling in Ansible:

## Ignoring Errors
To ignore errors and allow the playbook to continue, use the ignore_errors directive.

```
- name: Install a package
  apt:
    name: non-existent-package
    state: present
  ignore_errors: yes
```

## Handling Task Failures
Ansible provides several ways to handle task failures:

### Using failed_when
The failed_when directive allows you to specify a condition that determines if a task has failed.

```
- name: Check if a file exists
  stat:
    path: /path/to/file
  register: file_check

- name: Fail if the file does not exist
  debug:
    msg: "The file exists."
  failed_when: not file_check.stat.exists
```

### Using rescue and always
The block, rescue, and always directives provide a way to handle tasks that might fail and perform cleanup 
actions.

```
- name: Attempt a task and handle failure
  block:
    - name: Try to install a package
      apt:
        name: non-existent-package
        state: present
  rescue:
    - name: Handle the failure
      debug:
        msg: "The package installation failed, performing recovery."
  always:
    - name: Always run this task
      debug:
        msg: "This task runs regardless of success or failure."
```

### Using register to Capture Task Results
The register directive captures the result of a task in a variable, which can be used for conditional error 
handling.

```
- name: Run a command
  command: /bin/false
  register: command_result
  ignore_errors: yes

- name: Check the result of the command
  debug:
    msg: "The command failed with return code {{ command_result.rc }}"
  when: command_result.failed
```

## Retrying Failed Tasks
The retries and delay directives allow you to retry a task a specified number of times with a delay between 
attempts.

```
- name: Try to install a package with retries
  apt:
    name: package-name
    state: present
  retries: 3
  delay: 5
  until: result is succeeded
  register: result
```

## Custom Failure Messages
You can provide custom failure messages using the msg directive in combination with failed_when.

```
- name: Check if a service is running
  service:
    name: non-existent-service
    state: started
  register: service_result
  failed_when: service_result.failed
  msg: "Custom failure message: The service could not be started."
```

## Example Playbook
Here's an example playbook that demonstrates various error handling techniques:

```
---
- name: Error Handling Example
  hosts: all
  tasks:
    - name: Attempt to install a package and ignore errors
      apt:
        name: non-existent-package
        state: present
      ignore_errors: yes

    - name: Register command result and handle failure
      command: /bin/false
      register: command_result
      ignore_errors: yes

    - name: Display failure message if command fails
      debug:
        msg: "The command failed with return code {{ command_result.rc }}"
      when: command_result.failed

    - name: Use block and rescue to handle failures
      block:
        - name: Try to install a package
          apt:
            name: non-existent-package
            state: present
      rescue:
        - name: Handle the failure
          debug:
            msg: "The package installation failed, performing recovery."
      always:
        - name: Always run this task
          debug:
            msg: "This task runs regardless of success or failure."

    - name: Retry task on failure
      shell: /bin/false
      register: result
      retries: 3
      delay: 5
      until: result.rc == 0
      ignore_errors: yes

    - name: Custom failure message
      shell: /bin/false
      register: custom_result
      failed_when: custom_result.rc != 0
      msg: "Custom failure message: The command did not succeed."
```      

By incorporating these error-handling techniques, we can create more resilient and reliable Ansible playbooks.
