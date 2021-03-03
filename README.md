# yum

## repo
```
yum repolist all
yum history info git
yum list
yum list --showduplicates git
```

## Add and enable a new repo
```
# Add Repo in /etc/yum.repos.d/...
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

cat /etc/yum.repos.d/elasticsearch.repo
[elasticsearch]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
autorefresh=1
type=rpm-md

# Install by enable elasticsearch repo
yum install --enablerepo=elasticsearch elasticsearch
```


## yum group
* https://access.redhat.com/documentation/fr-fr/red_hat_enterprise_linux/7/html/system_administrators_guide/sec-working_with_package_groups
```bash
yum group list
yum group install MATE
yum group info MATE
```

## yum history
```
yum history list all
Modules complémentaires chargés : fastestmirror
ID     | Ligne de commande        | Date et heure    | Action         | Modifié
-------------------------------------------------------------------------------
    13 | install net-tools.x86_64 | 2021-03-03 18:53 | Install        |    1
    12 | install vim              | 2020-01-22 00:16 | Install        |   32
    11 | install mod_ssl          | 2020-01-20 18:41 | Install        |    1
    10 | install httpd            | 2020-01-20 18:13 | Install        |    6
     9 | install openssl          | 2020-01-20 08:53 | Install        |    2
     8 | install fail2ban-systemd | 2020-01-20 01:07 | Install        |    1
     7 | install fail2ban         | 2020-01-20 00:54 | Install        |   20
     6 | update                   | 2020-01-20 00:54 | Update         |    1
     5 | install epel-release     | 2020-01-20 00:53 | Install        |    1
     4 | install --quiet --assume | 2020-01-19 19:37 | Install        |   16
     3 | -y install cronie cronie | 2020-01-18 08:16 | Install        |   65 EE
     2 | -y update                | 2020-01-18 08:16 | Update         |   14
     1 | --disablerepo=* --enable | 2020-01-18 08:14 | Install        |   96
history list

yum history info httpd
```
