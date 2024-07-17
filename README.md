# Description 

## Table of Contents
- [Prerequisite](#prerequisite)
- [How it works](#how-it-works)
- [Run](#run)

## Prerequisite
- Python
- Ansible
- Access token to your Hub with ```:read``` privileges

## How it works

## Run
### Get the playbook
```
git clone 
cd 
```
### Edit commons vars
Go to vars/base.yaml and specify list of repos:
```yaml
repos:
  - gitlab # for regular repos
  - infra/gitlab # for repos under a group or organization
```

Then change default path for backup directory and archive:
```yaml
backup:
  dir: /home/server/backup/repos # space for playbook's work. Will be deleted on finish
  archive: /home/server/backup/rp-back # path to backup archive (without any extensions)
```

### Edit sensative vars
Rewrite values in vars/vault.yaml:
```sh
hub:
  address: github.com # domain name of a hub where your code is stored
  username: nolan 
  token: police@!$la!pd%set # access token with :read privileges
```

You can pass next steps in case you don't care about security or you are totaly sure these vars won't go anywhere.

Seal data using ansible-vault command and set password on prompt:
```sh
ansible-vault encrypt vars/vault.yaml
```

Use these to update values or just check them:
```sh
ansible-vault edit vars/vault.yaml 
ansible-vault view vars/vault.yaml 
```

If you want to change a pass for the vault:
```sh
ansible-vault rekey vars/vault.yaml 
```

### Run
Run playbook:
```sh
ansible-playbook main.yaml --ask-vault-pass # if you sealed the vault
ansible-playbook main.yaml # if you didn't
```





