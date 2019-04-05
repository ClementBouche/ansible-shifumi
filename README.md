# ansible-shifumi

## Requirements

* Install ansible

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get install ansible
```

## Local env

### Create new "localhost" inventory

* Copy `inventories/localhost-template` to `inventories/localhost`
```bash
cp inventories/localhost-template inventories/localhost
```
* Update variables `inventories/localhost/group_vars/all/vars.yml`
* Test ansible

```bash
ansible-playbook -i inventory/localhost test-echo.yml
# or
ansible -i inventory/localhost all -a "echo ShiFuMi"
```

## Remote env

### Update your remote connection info

* Add shifumi ssh connection information in ``~/.ssh/config``

```
host    shifumi
        HostName XXX.XXX.XXX.XXX
        User XXX
```

* Run ssh copy id

```bash
ssh-copy-id shifumi
```

### Test ansible

```bash
ansible-playbook -i inventory/remote test-echo.yml
# or
ansible -i inventory/remote all -a "echo ShiFuMi"
```

### Import roles

```bash
ansible-galaxy install -r requirements.yml -p roles --force
```

## Scripts

### Install / Update Soft

```bash
ansible-playbook -i inventory/remote install.yml --ask-vault
```


### Deploy webapp

```bash
ansible-playbook -i inventory/remote webapp.yml --ask-vault
```
