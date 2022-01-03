# Deploy a Production Ready Cloudera Cluster

![Cloudera Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Cloudera_logo_darkorange.png/640px-Cloudera_logo_darkorange.png)

If you have questions, check the documentation at [docs.cloudera.com](https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/index.html)

## Quick Start

To deploy the cluster you can use :

### Current release
0.1

### OS

#### OS version

* [x] CentOS 7 / RedHat 7
* [ ] Ubuntu 18
* [ ] Ubuntu 20

### Ansible

#### Ansible version

Ansible 2.9.25 it was tested cluster deployment to cloudera

### Preparatory nodes settings

```ShellSession
# Stop and Disable firewalld
systemctl stop firewalld
systemctl disable firewalld

# Stop and Disable SELinux
sed -i.bak 's/.*=enforcing.*/SELINUX=disabled/' /etc/selinux/config ; sed -i.bak 's/.*=permissive.*/SELINUX=disabled/' /etc/selinux/config 
setenforce 0

# Disable IPv6
echo 'net.ipv6.conf.all.disable_ipv6 = 1' >> /etc/sysctl.conf
echo 'net.ipv6.conf.default.disable_ipv6 = 1' >> /etc/sysctl.conf
sysctl -p
```

### Variables to be changed

#### Path to archive cloudera and Web server address
Path = roles/create_repo/vars/main.yml

```
archive_file: PATH_TO_YOUR_ARCHIVE
web_server_address: YOUR_WEB_SERVER_ADDRESS
```

#### Password for your users and databases
Path = roles/configure_data_bases/vars/main.yml

```
PASSWORD: YOUR_PASSWORD_FOR_USERS_AND_DATABASES
```

#### Tuning postgresql.conf (optional)
##### Used PostgreSQL 10
Uncomment the desired PostgreSQL configuration and comment out the unnecessary PostgreSQL configuration.
<br/>
The default is **postgresql-small.conf**
<br/>
<br/>
Path = roles/install_and_configure_postgresql/vars/main.yml

```
postgresql_config: postgresql-small.conf
#postgresql_config: postgresql-large.conf
```

### Deploy cluster

```ShellSession
sh _deploy_cluster.sh {username}
```
