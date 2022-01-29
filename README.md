# yum-rpm

## dnf
```
sudo dnf update
wget https://atom.io/download/rpm -O atom.x86_64.rpm
sudo dnf localinstall atom.x86_64.rpm
```

## rpm
```
## Dependencies
# rpm -qp atom.rpm --requires
(glib2 or kde-cli-tools or xdg-utils)
(libcurl.so.3()(64bit) or libcurl.so.4()(64bit))
alsa-lib
git-core
gtk3
libX11-xcb.so.1()(64bit)
libXss.so.1()(64bit)
libgbm.so.1()(64bit)
libgcrypt.so.20()(64bit)
libnotify
libnss3.so()(64bit)
libsecret-1.so.0()(64bit)
libxcb-dri3.so.0()(64bit)
libxkbfile.so.1()(64bit)
lsb-core-noarch
polkit
rpmlib(CompressedFileNames) <= 3.0.4-1
rpmlib(FileDigests) <= 4.6.0-1
rpmlib(PayloadFilesHavePrefix) <= 4.0-1
rpmlib(RichDependencies) <= 4.12.0-1

## show providers
# rpm -qp atom.rpm --provides
atom = 1.58.0-0.1
atom(x86-64) = 1.58.0-0.1

```


## yum repo
```
yum list installed

yum repolist all
yum history info git
yum list
yum list --showduplicates git

yum  whatprovides netstat
Dernière vérification de l’expiration des métadonnées effectuée il y a 4:01:23 le lun. 25 oct. 2021 20:54:51 CEST.
net-tools-2.0-0.52.20160912git.el8.x86_64 : Basic networking tools
Dépôt               : baseos
Correspondances trouvées dans  :
Nom de fichier : /usr/bin/netstat
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

yum history package-list httpd
Modules complémentaires chargés : fastestmirror
ID     | Action         | Package
-------------------------------------------------------------------------------
    10 | Installation   | httpd-2.4.6-90.el7.centos.x86_64
history package-list
```
