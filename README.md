Image for running Oracle Database 11.2.0.1(cover version of jaspeen / oracle-11g).

First Of All, Respect to [jaspen](https://github.com/jaspeen/oracle-11g).

The jaspeen / oracle-11g is used to establish the oracle server which is version 11.2.0.4 based,
but accourding to the Oracle, since 11.2.0.1 is now the only supported version of oracle11g on linux , I did some small changes.

Due to oracle license restrictions image is not contain database itself and will install it on first run from external directory.

>This image for development use only.

**Changes**

1. Fix it to fit the verion 11.2.0.1.

2. Modify /assets/install.sh replace the below content:(`nothing changes functionally`)
```bash
su oracle -c "/install/database/runInstaller -silent -ignorePrereq \
-waitforcompletion -responseFile /assets/db_install.rsp"
```
with
```
su oracle -c "/assets/run_installer.sh"
```

**Usage**

Download database installation files from [Oracle site](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html#11g) and unpack them to install_folder. 

Run container and it will install oracle and create database:

```bash
sudo docker run --privileged --name oracle11g -p 1521:1521 \
-v <install_folder>:/install -v <local_foloder>:/opt/oracle/app \
shuu1208/oracle11g
```
**Notice:**

The `"-v <local_foloder>:/opt/oracle/app"` is for persistent data.

```bash
sudo mkdir -p -m 755 <local_foloder>
sudo chown -R 440:220 <local_foloder>
```

Then you can commit this container to have installed and configured oracle database:
```bash
sudo docker commit -m "oracle11g-installed" ora11g
```
Database located in /opt/oracle folder

OS users:

root/redhat
oracle/oracle
DB users:

SYS/system
SYSTEM/system
