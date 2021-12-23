# Deploy a Production Ready Cloudera Cluster

![Cloudera Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Cloudera_logo_darkorange.png/640px-Cloudera_logo_darkorange.png)

If you have questions, check the documentation at [docs.cloudera.com](https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/index.html)

## Quick Start

To deploy the cluster you can use :

### Current release
7.1.7

### Ansible

#### Ansible version

Ansible v2.7.5 it was tested cluster deployment to cloudera

#### Preparatory nodes settings

```ShellSession
# Stop and Disable firewalld
systemctl stop firewalld
systemctl disable firewalld

# Stop and Disable SELinux
sed -i.bak 's/.*=enforcing.*/SELINUX=disabled/' /etc/selinux/config ; sed -i.bak 's/.*=permissive.*/SELINUX=disabled/' /etc/selinux/config 
setenforce 0
```

#### Variables to be changed

```
# Path to archive cloudera
# Path = roles/create_repo/vars/main.yml
archive_file: PATH_TO_YOUR_ARCHIVE

# Passwords for your databases and users
sed -i 's/YOUR_PASSWORD_FOR_USERS_AND_DATABASES/ExaMpLe_Pa$$w0rd/' roles/configure_data_bases/vars/main.yml
```

#### Deploy cluster
```ShellSession
sh _deploy_cluster.sh ``username``
```
