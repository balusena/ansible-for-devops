# 1. Check Ansible-Vault Installed in your machine:

```
ubuntu@balasenapathi~ ansible-vault

Usage: ansible-vault [create|decrypt|edit|encrypt|encrypt_string|rekey|view] [options] file_name

Options:
  --ask-vault-pass      ask for vault password
  --vault-id VaultID@source specify the vault identity to use
  --new-vault-id VaultID@source specify a new vault identity to use for rekey
  --vault-password-file VAULT_PASSWORD_FILE
                        vault password file
  --output OUTPUT_FILE  output file name for encrypt or decrypt; use - for
                        stdout
  --encrypt-vault-id ENCRYPT_VAULT_ID
                        the vault id to use for encryption; required if using
                        --encrypt-string
  --in-place            edit file in place (default for encrypt and decrypt)
  -h, --help            show this help message and exit

  Actions:
    create              Create new file and encrypt it
    decrypt             Decrypt specified file(s)
    edit                Edit specified file(s)
    encrypt             Encrypt specified file(s)
    encrypt_string      Encrypt specified string(s)
    rekey               Re-key specified file(s) to use a new password
    view                View the contents of the specified encrypted file

  See 'ansible-vault <command> --help' for more information on a specific command.
```

# 2. Now we are creating a file and keep in a place where all our hosts can access i.e group_vars
```
ubuntu@balasenapathi~ ls 
ec2	ec2_create.yaml     group_vars    inventory.ini    vault.pass

ubuntu@balasenapathi~ cd group_vars

ubuntu@balasenapathi/group_vars~ ls
all app.yaml

ubuntu@balasenapathi/group_vars/all~ ls	

ubuntu@balasenapathi/group_vars/all~ vim aws_credentails.yaml
~ec2_access_key: marmaraluatukulu
~ec2_secret_key: atukulumarmaralu
:wq

ubuntu@balasenapathi/group_vars/all~ openssl rand -base64 2048 > vault.pass
NmVtWVdRUExhYnpVc3Q3U0pzKzJic1ZHTEFvMkxtb21CVnNSSkVzMk9FS0lFUXhrRWlpS3o1Nmts
Nm5aQ1BsM0dpS0g4WE5qNjFLNE85WE1mczQ4RWpmWVRtcFBPYlpnbkJtL0xFejFFVHpJVXdnRXZW
eU1XVjZHRFdpY3Nsd1VCaXhFTTQxSmQ4NnFtZUlPRXViWUJ6MGxuQmZyY0hKT3Z4dzlSeVpyUGFq
Nk9oalhuK2YwMElPMW4vTHprbDJ2S2pBT1V5UmFhWm1IMzhrZ2t6QzI1MDFONjZRa3pGblNLT3ZT
R1pyeGFUbEluVmJYZWVsQXp3cDNXWnp2c2oyTFdTZHZPb0lvZ0xkZlhOdm5FS2FSdFdNMlZXZmMy
c0t2VGtLbXRmQmlJcHZaTW1Sckw0UklreUpIMnNOUU1EUDc1ek01T2pQYkVZNGwvM0NRSkhZZU9a
YjN5a2tvblQ5Smx0UXJhZVFQWnJxdXJMSkxzMlVvUmlOMm1FZm94SEJlRmVKaHlVQThDNTNkeC9N
czZSSVkvT0JHRThKUDhSYU9iUU5oR2YyVVVYb3JxNjk4WWJKMHRvaHpoN1dxS0VnVzZPdDZhdEov
WXpVSEY1NE1ZYkxSMVJQeENLY0FUM3lvTmhweVg3WWw5UkFQeTgwM3RYRVRJeExocXc1ZXV1YUJY
RUp2N2Nyb1lIV2hUMmtlNEg5cUlva3VQQlU4ZXJ3MGQvN2RSbGdUVGFWdjNTeXh4dXNrbTQ2QkpP
bUNlUzkrdHVnbmtmNm9MYVpNTHd6T0U3aUZnd1ppM1lZajkzRmlhQlJPMUhqWG0zRzZZMk42RTdu
aTczU1lYMEFmVnh1RUVPVll2bFVhMVdhUUY2L09LdVN3NmJ1QU1uU25FUUxZY1ZqVE9Xbk5nOWpk
cWxTaGcrdnByVGV4WUxGNHpLTlQrL1d1SGhaRWJ2Q0JueGhuU1Z6T3ZwQXVFeFdKdStReG9raXJo
dE9ydjFYajdxaTNSekZyTFMwQ0tkRjlydE9Hb0JqQ2ljOU92R0dlclcxS0JzNG1JZUF2QVNQdG1Q
Y1lMQWRkK2pST3R0b3pWOUdPTi94ME5KdXlwZ2ZDbzNCRi8xdzZPZWdDaFZOdHFIdHc2Ykd0cG1k
QnpncGVnVkpGVnRUZnFjRHd5bU1FRldVYm5idkExa2dBVzNMTU9YcThtMG9qTkRmckdpd3hlUEYv
SkVPUkJjdFpGcDdybnk3QU5lTzJmOTdwNks2aHRkZkpuOTh0M2lWT1ZxL1BHZnZ4dW9mSkdHRTht
U0Z1dGxsU1E1WmMvL3piOUxSYWV5cFpvczZGU0FnVjZPN21wQnQxY3l1YVViRFV1dytYYmZBU05S
azUzb3FXcW5uL3lFVnpzbDZydklJVnd2cGZFWlpmNGh2aG1jNG1JUE5HV0pNSm9GVTVXOHN5RStx
NVd1THJvd2xPd2ViMW50bnhScjBWTVhJbFVEQXlra0xLY1ZlajFtNStxMW5WNXlPbHd2Q3Nta1ZD
ZjIvVnI4L3VWVTdhTVhxdlhZV3RzZ0RWM0hqS0h1L3FzWkdNWHUyb0lLYXdpYURMRllnWjh0ZStp
RE5kRHpxUWRkcGJqZGpqLzNCOTNrQ1ZKNWc5WklycEttSHQ5eTlxTnFzT1BlQXZqNmVnNW1vMjdD
WkNFNHl5bG03UXczanVXbW0wMjNHNmdIZTBpTzFtaFZZNGZ1Q0JFcE1VQXhYMjRFTTRrVWZnaWxo
SmtUV2pVc0czNnliWEo4Y1VwckI2dTZWSTBHRWlxL2xhNTdBSktneTVDZVpIMElYekNQYXJlMXZr
OU9qZ0ZaYzY5YklPYTFyZ3pzdEd0ZEpMdENmRlRRUVhVQmhsOGdvM1hVS2lQdm8zbWpVQlMxdmVP
WEFtaG5pK2pSQW12QWVScEF0TzE3MjYvclR5M3dKTTJ1U3JwMStsb1lUUm1kNTh5a2J3eE5mMzN1
TEFGMGU4WTVHb0NaekFtVFNkcHRvOEtVT3ZGbGp3TkVrTklZQUxrLzhtRXJYWUlNS0MwbG93ZmVm
ZFYwTlJZT1llOHdCaG9nYlE4b1pzN0NzSVh4akNHSDkxOVdMQ1Y2WkFsWjN1OFlrVWt6UXpsUVFo
d2Ixem5GeUNFSzFkZ09xMXFjWVFMYzdCaU5IUlRZTkpaNUNQSmRrSkFiRWNadVJhUG9kM0grcWxy
a1JUS3c3S2hzOHpoOU1nNkU5RUQwVWljT3ZTV21jWW42N3ZvbHZpMG0vVnp2RmJheGZqZkpiRHN2
K2VsdnJGTUhrOXZ2N3VVUjNiZy95cTl1d0s1NVZqS2I1UjVYdzY0YzZhdWhKZmFiZkNQK1FuQmpP
algrb0hwcDRlazhlcllPZVViZ0t1U3RLbFhLRDhMWlB0TW8zQ0ZreEhXVlJ2ZXZlNFJaajMrMzVp
TVdyVEdtU1pUeHpzZnZrVDRWRXVCU2pGZVZZbTV5b3Z2K2c2eVFIM2dUSnVZMG42ODhoRU93U1h3
dDgrZDF0YkExVlp2K3Y5NlFoNE9wTElSVk5mV2dGQjlmY2Z6czdpdVBnMWppdDViNmNsc0k2L0Ju
QjBtZE9QQ3pwVm1OY1o4Y0NMR2VwOHdpSWhWcXRYcm42TjMxZEtSWEp6aGVUOW5KUDIvZldieGpW
OFdvOTY4aHFuWTh0RUtDbjNpeU5xcGNnN3ZRTlVvRVR2MlZmYXdtS1

ubuntu@balasenapathi/group_vars/all~ ls
aws_credentails.yaml pass.yml
```

- Note: Now if we upload this file to git repository then the AWS credentials are compromised, instead of this we
  are creating the file and password using Ansible Vault.

# 3. Now create the file and password using Ansible Vault.

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault create aws_credentials.yaml
New Vault Password:
```
- Note: We can also provide the password here using the Ansible Vault CLI

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault create aws_credentials.yaml --vault-password-file ../../vault.pass
~ec2_access_key: marmaraluatukulu
~ec2_secret_key: atukulumarmaralu
:wq
```
- Note: Ansible Vault Opens a file as shown above we can create the aws_credentials here securely

##  Encryption

- To see the aws_credentials.yaml file encrypted by Ansible Vault

```
ubuntu@balasenapathi/group_vars/all~ cat aws_credentials.yaml
$ANSIBLE-VAULT:1.1:AES256
6162636465666768696a6b6c6d6e6f707172737475767778797a30313233343536373839304142434445464748494a4b4c4d4e4f505
152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4f505152535455565758595a3132333435363738
39303142434445464748494a4b4c4d4e4f505152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4f5
05152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4f505152535455565758595a31323334353637
3839303142434445464748494a4b4c4d4e4f505152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4
f505152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4f505152535455565758595a313233343536
373839303142434445464748494a4b4c4d4e4f505152535455565758595a313233343536373839303142434445464748494a4b4c4d4
e4f505152535455565758595a313233343536373839303142434445464748494a4b4c4d4e4f505152535455565758595a3132333435
36373839303142434445464748494a4b4c4d4e4f505152535455565758595a313233343536373839303142434445464748494a4b4c4
d4e4f505152535455565758595a313233343536373839303142434445464748494
```
- Note: Now our aws_credentials.yaml file is encrypted by Ansible Vault.

## Decryption

- To see the aws_credentials.yaml file decrypted by Ansible Vault

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault decrypt aws_credentials.yaml --vault-password-file ../../vault.pass
Decryption Successful
```
- To see the aws_credentials.yaml file encrypted by Ansible Vault

```
ubuntu@balasenapathi/group_vars/all~ cat aws_credentials.yaml
ec2_access_key: marmaraluatukulu
ec2_secret_key: atukulumarmaralu
```

## Edit

- To edit the aws_credentials.yaml file encrypted by Ansible Vault to add the api_token

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault edit aws_credentials.yaml --vault-password-file ../../vault.pass
~ec2_access_key: marmaraluatukulu
~ec2_secret_key: atukulumarmaralu
~api_token     : luluatukumarmara
:wq
```

## View

- To view the secured information without encrption

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault view aws_credentials.yaml --vault-password-file ../../vault.pass
ec2_access_key: marmaraluatukulu
ec2_secret_key: atukulumarmaralu
api_token     : luluatukumarmara
```

## Encrypt

- The file is already created and stored in the specific location and now we are encrypting the existing file.

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault encrypt aws_credentials.yaml --vault-password-file ../../vault.pass
```

## Encrypt_String

- The file is already created and if we want to do specific change for any string in the existing file.

```
ubuntu@balasenapathi/group_vars/all~ ansible-vault encrypt_string ec2_access_key --vault-password-file ../../vault.pass
Encryption successful
!vault |
$ANSIBLE_VAULT;1.1;AES256
38666338383838386561376165616230626232376633383037373737656430396434656162383039
6430623338373430356539303932646539623163363234620a353335653861353731383165353337
66336631363430393465653335636263303137333061376665633633313335323031396130326330
6635653737666338360a393130666234653933303765343734306161356231376166376636386430
3535
```

# Best Practices for Ansible Vault Passwords

- Use Strong Passwords: Ensure passwords are complex and lengthy.
- Store in AWS Secrets Manager: Securely store Ansible Vault passwords in AWS Secrets Manager.
- Separate Passwords for Environments: Use different passwords for DEV, UAT, and PROD environments. Secure the PROD password in AWS Secrets Manager with appropriate
  AWS roles and policies to control access. This approach enhances security and minimizes the risk of unauthorized access to sensitive information.



