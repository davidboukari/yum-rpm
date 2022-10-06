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

* Which package contains this file
``` 
rpm -qf /etc/logrotate.d
logrotate-3.8.6-19.el7.x86_64
```


* List files in installed rpm
```
rpm -ql logrotate-3.8.6-19.el7.x86_64
/etc/cron.daily/logrotate
/etc/logrotate.conf
/etc/logrotate.d
/etc/rwtab.d/logrotate
/usr/sbin/logrotate
/usr/share/doc/logrotate-3.8.6
/usr/share/doc/logrotate-3.8.6/CHANGES
/usr/share/doc/logrotate-3.8.6/COPYING
/usr/share/man/man5/logrotate.conf.5.gz
/usr/share/man/man8/logrotate.8.gz
/var/lib/logrotate
/var/lib/logrotate/logrotate.status
```

* extract an rpm
```
rpm2cpio php-5.1.4-1.esp1.x86_64.rpm | cpio -idm
```



## Create a personal yum repo

* local repo
```
# install createrepo
# https://www.percona.com/blog/2020/01/02/how-to-create-your-own-repositories-for-packages/

mkdir mylocalrepo/{base,added}
cp *.rpm mylocalrepo/base
cp myapp.rpm mylocalrepo/added

createrepo mylocalrepo

# Configure httpd to /mylocalrepo


# On the node
yum clean all
# probably desable package
yum -y disable mypackage
yum search mypackage

yum info mypackage

```

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




## Security
* List update sec
```

yum updateinfo list security
Dernière vérification de l’expiration des métadonnées effectuée il y a 0:01:29 le mar. 06 sept. 2022 09:15:19 CEST.
FEDORA-EPEL-2022-3a6675bd1a Sécurité/Niveau important. chromium-102.0.5005.115-1.el8.x86_64
FEDORA-EPEL-2022-3a6675bd1a Sécurité/Niveau important. chromium-common-102.0.5005.115-1.el8.x86_64


yum updateinfo list security installed
Dernière vérification de l’expiration des métadonnées effectuée il y a 0:05:16 le mar. 06 sept. 2022 09:15:19 CEST.
FEDORA-EPEL-2022-3a6675bd1a Sécurité/Niveau important. chromium-102.0.5005.115-1.el8.x86_64
FEDORA-EPEL-2022-3a6675bd1a Sécurité/Niveau important. chromium-common-102.0.5005.115-1.el8.x86_64
```



* Info sec
```
yum info-sec
Dernière vérification de l’expiration des métadonnées effectuée il y a 0:02:10 le mar. 06 sept. 2022 09:15:19 CEST.
===============================================================================
  chromium-102.0.5005.115-1.el8
===============================================================================
ID de mise à jour: FEDORA-EPEL-2022-3a6675bd1a
             Type: sécurité
       Mis à jour: 2022-07-01 02:44:47
        Anomalies: 2035520 - Please branch and build chromium for EPEL 9
                 : 2071876 - CVE-2022-1232 chromium-browser: Type Confusion in V8
                 : 2071878 - CVE-2022-1232 chromium: chromium-browser: Type Confusion in V8 [epel-all]
                 : 2076274 - CVE-2022-1364 Chromium-browser: Type Confusion in V8.
                 : 2076451 - CVE-2022-1364 chromium: Chromium-browser: Type Confusion in V8. [epel-all]
                 : 2084016 - CVE-2022-1633 chromium-browser: Use after free in Sharesheet
                 : 2084017 - CVE-2022-1634 chromium-browser: Use after free in Browser UI
                 : 2084018 - CVE-2022-1635 chromium-browser: Use after free in Permission Prompts
                 : 2084019 - CVE-2022-1636 chromium-browser: Use after free in Performance APIs
                 : 2084020 - CVE-2022-1637 chromium-browser: Inappropriate implementation in Web Contents
                 : 2084021 - CVE-2022-1638 chromium-browser: Heap buffer overflow in V8 Internationalization
                 : 2084022 - CVE-2022-1639 chromium-browser: Use after free in ANGLE
                 : 2084023 - CVE-2022-1640 chromium-browser: Use after free in Sharing
                 : 2084024 - CVE-2022-1641 chromium-browser: Use after free in Web UI Diagnostics
                 : 2084026 - CVE-2022-1633 CVE-2022-1634 CVE-2022-1635 CVE-2022-1636 CVE-2022-1637 CVE-2022-1638 CVE-2022-1639 CVE-2022-1640 CVE-2022-1641 chromium: various flaws [epel-all]
                 : 2090284 - CVE-2022-1853 chromium-browser: Use after free in Indexed DB
                 : 2090285 - CVE-2022-1854 chromium-browser: Use after free in ANGLE
                 : 2090286 - CVE-2022-1855 chromium-browser: Use after free in Messaging
                 : 2090287 - CVE-2022-1856 chromium-browser: Use after free in User Education
                 : 2090288 - CVE-2022-1857 chromium-browser: Insufficient policy enforcement in File System API
                 : 2090289 - CVE-2022-1858 chromium-browser: Out of bounds read in DevTools
                 : 2090290 - CVE-2022-1859 chromium-browser: Use after free in Performance Manager
                 : 2090291 - CVE-2022-1860 chromium-browser: Use after free in UI Foundations
                 : 2090292 - CVE-2022-1861 chromium-browser: Use after free in Sharing
                 : 2090293 - CVE-2022-1862 chromium-browser: Inappropriate implementation in Extensions
                 : 2090294 - CVE-2022-1863 chromium-browser: Use after free in Tab Groups
                 : 2090295 - CVE-2022-1864 chromium-browser: Use after free in WebApp Installs
                 : 2090296 - CVE-2022-1865 chromium-browser: Use after free in Bookmarks
                 : 2090297 - CVE-2022-1866 chromium-browser: Use after free in Tablet Mode
                 : 2090298 - CVE-2022-1867 chromium-browser: Insufficient validation of untrusted input in Data Transfer
                 : 2090299 - CVE-2022-1868 chromium-browser: Inappropriate implementation in Extensions API
                 : 2090300 - CVE-2022-1869 chromium-browser: Type Confusion in V8
                 : 2090303 - CVE-2022-1870 chromium-browser: Use after free in App Service
                 : 2090304 - CVE-2022-1871 chromium-browser: Insufficient policy enforcement in File System API
                 : 2090305 - CVE-2022-1872 chromium-browser: Insufficient policy enforcement in Extensions API
                 : 2090306 - CVE-2022-1873 chromium-browser: Insufficient policy enforcement in COOP
                 : 2090307 - CVE-2022-1874 chromium-browser: Insufficient policy enforcement in Safe Browsing
                 : 2090308 - CVE-2022-1875 chromium-browser: Inappropriate implementation in PDF
                 : 2090309 - CVE-2022-1876 chromium-browser: Heap buffer overflow in DevTools
                 : 2090313 - CVE-2022-1853 CVE-2022-1854 CVE-2022-1855 CVE-2022-1856 CVE-2022-1857 CVE-2022-1858 CVE-2022-1859 CVE-2022-1860 CVE-2022-1861 CVE-2022-1862 CVE-2022-1863 CVE-2022-1864 CVE-2022-1865 CVE-2022-1866 CVE-2022-1867 ... chromium: various flaws [epel-all]
      Description: Update to Chromium 102.0.5005.115 (yes, I know there is a newer one, but we need to get something out now).
                 :
                 : This also adds the first build of Chromium for EPEL9, many thanks to all the folks who got the many dependencies built.
                 :
                 : Fixes:
                 : CVE-2022-1232 CVE-2022-1364 CVE-2022-1633 CVE-2022-1634 CVE-2022-1635 CVE-2022-1636 CVE-2022-1637 CVE-2022-1638 CVE-2022-1639 CVE-2022-1640 CVE-2022-1641 CVE-2022-1853 CVE-2022-1854 CVE-2022-1855 CVE-2022-1856 CVE-2022-1857 CVE-2022-1858 CVE-2022-1859 CVE-2022-1860 CVE-2022-1861 CVE-2022-1862 CVE-2022-1863 CVE-2022-1864 CVE-2022-1865 CVE-2022-1866 CVE-2022-1867 CVE-2022-1868 CVE-2022-1869 CVE-2022-1870 CVE-2022-1871 CVE-2022-1872 CVE-2022-1873 CVE-2022-1874 CVE-2022-1875 CVE-2022-1876
        Criticité: Important

===============================================================================
  epel-release-8-17.el8
===============================================================================
ID de mise à jour: FEDORA-EPEL-2022-96fd03a1b9
             Type: correction d’anomalie
       Mis à jour: 2022-08-20 02:40:43
      Description: Tweak crb script, Recommends dnf-command(config-manager) (#2115602)
        Criticité: None

===============================================================================
  htop-3.2.1-1.el8
===============================================================================
ID de mise à jour: FEDORA-EPEL-2022-b44b84c966
             Type: inconnu
       Mis à jour: 2022-07-31 04:19:05
        Anomalies: 2108676 - SIGSEGV in LinuxProcess_makeCommandStr()
      Description: - update to v3.2.1
        Criticité: None

===============================================================================
  ncdu-1.17-1.el8
===============================================================================
ID de mise à jour: FEDORA-EPEL-2022-f9fb8a9947
             Type: inconnu
       Mis à jour: 2022-06-11 04:13:15
      Description: Update to new version 1.17. Changes:
                 :
                 : * Add ‘dark-bg’ color scheme and use that by default
                 : * Use natural sort order when sorting by file name
                 : * Improve compatibility with C89 environments
                 : * Fix wrong assumption about errno not being set by realloc()
        Criticité: None

===============================================================================
  python-lz4-2.1.2-6.el8 python-pkgconfig-1.5.1-5.el8 python-psutil-5.6.3-5.el8 python-sphinx-bootstrap-theme-0.8.0-1.el8
===============================================================================
ID de mise à jour: FEDORA-EPEL-2019-6adf1e0ef3
             Type: nouveau paquet
       Mis à jour: 2019-10-25 19:27:48
        Anomalies: 1758794 - Branch request: python3-lz4 for epel8
      Description: Build for EPEL8
```






```
# yum updateinfo list security all
# yum updateinfo list sec

To list all available security updates with verbose descriptions of the issues they apply to:

# yum info-sec

Listing currently installed security updates

To get a list of the currently installed security updates this command can be used:

# yum updateinfo list security installed


```
