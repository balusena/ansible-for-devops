# Implementing Policy as Code to manage the versioning of an AWS S3 bucket using Ansible.

## 1. Create S3 buckets in AWS S3

- datametrics-mangroo-x
- middleware-logs-mangroo-x
- paymentapp-logs-mangroo-x

## 2.To configure AWS on Ansible Control machine i.e our ubuntu server where ansible is running.

### To run Ansible playbooks that manage AWS resources, including S3 buckets, the server running the playbooks needs AWS access. This can be achieved in different ways:

### 1. Using an IAM User with Permissions:

- Create an IAM user and grant it the necessary permissions to access the S3 bucket.
- Generate access keys (Access Key ID and Secret Access Key) for the IAM user.
- Use these access keys in your Ansible playbooks to authenticate and manage the S3 bucket.

### Using Root User Access Keys:

- Although it is possible to use the root user’s access keys to connect to AWS resources, it is not recommended due to security risks.
- Best practices dictate using IAM users or roles with the least privileges necessary for the tasks at hand.

### Connect to the AWS from server where we are running ansible playbook

```
ubuntu@balasenapathi:~$ aws configure
AWS Access Key ID [None]: your_access_key_id
AWS Secret Access Key [None]: your_secret_access_key
Default region name [None]: your_default_region
Default output format [None]: json 
```

### To list the all S3 buckets in our AWS account

````
ubuntu@balasenapathi:~$ aws s3 ls 
2024-07-01 09:00:00 datametrics-mangroo-x
2024-07-05 12:00:00 middleware-logs-mangroo-x
2024-07-10 15:30:00 paymentapp-logs-mangroo-x
````

- Note: Our s3 bucket versioning is disabled by default.

## 3. Install python3 and boto3 in your ubuntu instance where ansible is running because here ansible with
      
To set up an Ubuntu instance for running Ansible playbooks that interact with AWS S3 buckets, you need
to install Python3 and Boto3. Boto3 is the AWS SDK for Python, which allows Ansible to make API calls 
to AWS services, including S3. Here’s how to do it.

```
Update the Package List:

ubuntu@balasenapathi:~$ sudo apt update

Install python3

ubuntu@balasenapathi:~$ sudo apt install -y python3 python3-pip

Install boto3

ubuntu@balasenapathi:~$ pip3 install boto3

```

## 4.Install AWS collection where our ansible is running.

```
ubuntu@balasenapathi:~$ ansible-galaxy collection install amazon.aws
Process install dependency map
Starting collection install process
Installing 'amazon.aws:2.3.0' to '/home/ubuntu/.ansible/collections/ansible_collections/amazon/aws'
Downloading https://galaxy.ansible.com/download/amazon-aws-2.3.0.tar.gz to /home/ubuntu/.ansible/tmp/ansible-local-12345_abcdef/_ivj5y0f/amazon-aws-2.3.0-z6lcvmpv
amazon.aws:2.3.0 was installed successfully
```
## 5. Now run the ansible playbook that contains Policy as Code to manage the versioning of an AWS S3 bucket.

```
ubuntu@balasenapathi:~$ ansible-playbook 10-Policy as Code/s3_versioning.yaml

PLAY [Enforce s3 bucket versioning on AWS account] *****************************

TASK [List S3 buckets in AWS account] ******************************************
ok: [localhost]

TASK [debug] *******************************************************************
ok: [localhost] => {
    "result": {
        "buckets": [
            {
                "name": "datametrics-mangroo-x",
                "creation_date": "2024-07-01T09:00:00Z"
            },
            {
                "name": "middleware-logs-mangroo-x",
                "creation_date": "2024-07-05T12:00:00Z"
            },
            {
                "name": "paymentapp-logs-mangroo-x",
                "creation_date": "2024-07-10T15:30:00Z"
            }
        ],
        "changed": false,
        "failed": false
    }
}

TASK [Enable versioning on S3 bucket] ******************************************
changed: [localhost] => (item={'name': 'datametrics-mangroo-x', 'creation_date': '2024-07-01T09:00:00Z'})
changed: [localhost] => (item={'name': 'middleware-logs-mangroo-x', 'creation_date': '2024-07-05T12:00:00Z'})
changed: [localhost] => (item={'name': 'paymentapp-logs-mangroo-x', 'creation_date': '2024-07-10T15:30:00Z'})

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
















