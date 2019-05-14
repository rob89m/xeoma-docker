Run Xeoma with Docker
================

### Purpose
Xeoma (Security Monitoring Software) developed by Felena Soft http://felenasoft.com/, running in a Docker.

### EULA
Make sure you read this - http://felenasoft.com/xeoma/en/eula/ as you are effectively agreeing to it by running this docker.

### Getting the Docker
From Docker Index
```
docker pull rob89m/xeoma-docker
```

Build yourself
```
git clone https://github.com/rob89m/xeoma-docker.git
docker build --rm -t <your-docker-name>/xeoma xeoma-docker
```

### Running
To run the container, fire up docker like so:

```
$ sudo docker run -d --name="xeoma" --restart="always" --net=host -p 8090:8090 -v <local storage>:/usr/local/Xeoma -v /mnt/archive:/usr/local/Xeoma/XeomaArchive rob89m/xeoma-docker
```

If you want to store your archive somewhere other than in your docker container add another volume:
```
$ sudo docker run -d --name="xeoma" --restart="always" --net=host -p 8090:8090 -v <local storage>:/usr/local/Xeoma -v /mnt/archive:/usr/local/Xeoma/XeomaArchive rob89m/xeoma-docker
```

#### Password
The docker build process automatically creates a password on build, however it will also will generate a password the first time it runs.  It is then dumped to the log, so view it using:
```
docker logs xeoma
```

### Usage
To access your xeoma server, simply download the same version from http://felenasoft.com/xeoma/en/download/ and set it up to connect to a remote server using the password generated.  You can use it in a trial mode, however the free mode disables remote access, so pointless using with docker.  It's pretty great cheap software - give it a go!
Ensure you are using a volume before you install the license, otherwise if you need to stop/recreate or upgrade later, you will lose your license file (meaning you will need to contact FelenaSoft to reset it).

### Upgrading
 As long as you have your /usr/local/Xeoma mapped to a volume, then you can safely stop, remove and start up new containers.  Config/license is carried across between containers being recreated.

### Notes
Due to how many security cameras work, this needs to be on the host network stack.  This probably can be changed to not be so insecure, but I haven't done it yet.

### Support
I don't work for FelenaSoft, I just own a license.  So if you find any bugs with the software that are related to the docker container, let me know and I'll investigate.  If you find bugs that are related to the actual software or cameras, etc then contact FelenaSoft.  This project is a personal pet project that FelenaSoft is aware of, but offer no support for it.  Don't hassle them if things don't work in relation to the container, etc.

### Todo
Set up a better start up process, so it has config to disable upgrades (upgrades to the software should be performed through a new container, not by using the upgrade through Xeoma)
