# Comparison with Shell Scripting

- **Platform Dependency**: Shell scripting primarily works only for Linux and Unix-like systems. 

- **Complexity and Readability**: Shell scripts can become complex and less readable, especially for non-experts, as the script size increases.

- **Idempotence and Predictability**: Ansible is designed to be idempotent, meaning that if the system is already in the state described by the playbook, Ansible will not make any changes, even if the playbook runs multiple times. Shell scripts are generally not idempotent. For example, running the following shell script twice will cause it to fail, demonstrating its lack of idempotence:

    ```bash
    #!/bin/bash

    set -e 

    mkdir test-demo
    echo "hi"
    ```

- **Scalability and Flexibility**: Ansible can easily and quickly scale the systems you automate through its modular design, which supports a wide range of operating systems, cloud platforms, and network devices.


