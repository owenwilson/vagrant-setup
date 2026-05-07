# Vagrant virtual-box

## install vagrant
- check the install [documentation vagrant](https://developer.hashicorp.com/vagrant/install)

```sh
wget -O- https://rpm.releases.hashicorp.com/fedora/hashicorp.repo | sudo tee /etc/yum.repos.d/hashicorp.repo
sudo yum list available | grep hashicorp
sudo dnf -y install vagrant
```

## example first machine

### create ssh key
```sh
sshkeygen -t ed25519 -C "yourMachineName@domainEmail.local"
ssh-copy-id usuario@IP
```

- configure another port ssh
```sh
nano /etc/ssh/sshd_config
```
- uncomment port and change port
```sh
Port 2222
```
- enable port SELinux `RHEL/fedora`
```sh
sudo semanage port -a -t ssh_port_t -p tcp 2222
```
```sh
sudo firewall-cmd --add-port=2222/tcp --permanent
```
- remove default ssh port
```sh
sudo firewall-cmd --permanent --remove-service=ssh
```
```sh
sudo firewal-cmd --reload
```
- restart ssh service
```sh
sudo systemctl restart sshd
sudo systemctl status sshd
```


### configure port RHEL/Fedora

- check [vagrant tutorial setup project](https://developer.hashicorp.com/vagrant/tutorials/get-started/setup-project)
- check [portal cloud hashicorp](https://portal.cloud.hashicorp.com/vagrant/discover)
- start vagrantfile
```sh
vagrant init hashicorp-education/ubuntu-24-04 --box-version 0.1.0
```

- start the first virtual machine
```sh
cd folder_vagrant
ls -l Vagrantfile
vagrant up
```

## provide remote access and configuration
- install the plugin on the local host
```sh
vagrant plugin list
vagrant plugin install vagrant-managed-servers
```

- run command 
```sh
vagrant up --provider=managed
```


