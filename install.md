# OpenShift Origin Installation Instructions

#### Table of Contents
* [Linux](#linux)
* [Mac OS](#mac)
* [Windows 10](#windows)

<a name="linux"></a>
## Linux Setup (Tested on Fedora 24)

#### Install Openshift
* Navigate to https://github.com/openshift/origin/releases/tag/v3.6.0
* Scroll to the bottom of the page and select the download for your operating system
* In this case: **openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz**
* Once downloaded, in the terminal navigate to the download and extract the tar file
```
tar -xzvf openshift-origin-client-tools-v3.6.0c4dd4cf-linux-64bit.tar.gz
```
* Put **oc** file in **/usr/bin** directory (should already be in $PATH)
* The oc executable is located under the parent directory of the openshift-origin-client-tools  directory
* Put the **oc** file in /usr/bin directory
```
sudo mv ~/path/to/download/openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit/oc /usr/bin/
```
* To ensure the /usr/bin is on your path:
```
echo $PATH
```
  * Within your path you should see **...:/usr/bin:...**

#### Install Docker (version 1.12 or higher)
* Docker installation instructions for Fedora
   * https://docs.docker.com/engine/installation/linux/docker-ce/fedora/#install-docker-ce
* Set up the Repository
   * Run the following commands in the terminal
```
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo  https://download.docker.com/linux/fedora/docker-ce.repo
```

* Install docker with your platform's package manager
   * Since we are using Fedora as an example, the examples will use ‘**dnf**’ -- make sure to use the package manager for your specific distribution
```
sudo dnf install docker-ce
```
* Configure the docker daemon with an insecure registry parameter of 172.30.0.0/16

> If you have a registry secured with https but do not have proper certs
> distributed, you can tell docker to not look for full authorization by
> adding the registry to the INSECURE_REGISTRY line and uncommenting it.
> ```INSECURE_REGISTRY='--insecure-registry 172.30.0.0/16'```
  * Edit the /etc/sysconfig/docker file and add or uncomment this line -- ```INSECURE_REGISTRY='--insecure-registry 172.30.0.0/16'``` -- by running:
```
sudo vim /etc/sysconfig/docker
```
  * **OR** if you have version 17+ of docker edit the /etc/docker/daemon.json file or create the file if it does not exist and add the following:
```
{
     "insecure-registries": ["172.30.0.0/16"]
}
```

* Run the following after making these changes to restart docker:
```
systemctl daemon-reload
systemctl restart docker
```
> If you use your package manager to remove docker to start over `yum remove docker` make SURE to remove the docker files in /var/lib or else you will corrupt those files and not be able to start OC.


#### Run Openshift
* Start cluster:
```
oc cluster up
```
* Stop cluster:
```
oc cluster down
```

* When the cluster starts you should see the following: 

```
OpenShift server started.
The server is accessible via web console at:
    https://127.0.0.1:8443
You are logged in as:
    User:     developer
    Password: <any value>
To login as administrator:
    oc login -u system:admin
Access the web console at the url above :  https://127.0.0.1:8443
```

> If you receive an error that you cannot connect to the docker daemon you may need to run as root: ```sudo oc cluster up```

<a name="mac"></a>
## Setup for Mac (OS X El Capitan 10.11.6)

#### Install Docker
* https://docs.docker.com/docker-for-mac/install/
* Requires OS X El Capitan 10.11 or newer macOS release running on a 2010 or newer Mac
* Stable channel vs. Edge channel (Choose stable channel since it’s more supported)
* Double click Docker.dmg to open installer and drag icon into Applications folder
* Double click Docker app to start docker
* Check versions of Docker Engine, Compose, and Machine. Output may vary if you are running different versions:

```
docker --version
17.0.6.2-ce, build cec0b72
```
```
docker-compose --version
1.14.0, build c7bdf9e
```
```
docker-machine --version
0.12.2, build 9371605
```

* Add insecure registry of 172.30.0.0/16
  * From the Docker menu, select Preferences
  * Click on Daemon tab
  * Under Insecure registries, click on ‘+’ icon to add new entry
  * Enter 172.30.0.0/16
  * Click on Apply and Restart
* Install socat
  * If not installed already, install Homebrew for Mac
  * In Terminal, run: brew install socat
  * May need to change permissions and ownership of /usr/local:

```
chown -R $(whoami):admin /usr/local
```

#### Install Openshift
* Install oc binary using homebrew:
```
brew install openshift-cli
```

#### Run Openshift
* Start cluster:
```
oc cluster up
```
* Stop cluster:
```
oc cluster down
```


<a name="windows"></a>
## Setup for Windows 10

* Download links:
  * https://docs.docker.com/docker-for-windows/install/ (for Windows Pro/Enterprise)
  * https://www.docker.com/products/docker-toolbox (for Windows Home)
  * https://git-for-windows.github.io/ (for Windows Pro/Enterprise to have bash shell)
    * this is optional, but lets you have a convenient bash shell on Windows
  * https://github.com/openshift/origin/releases/tag/v3.6.0 (download exe file at bottom)

#### Install Openshift
* Move oc.exe file to ~/.oc with Git Bash
```
mv oc.exe ~/.oc
```

* Add oc CLI to PATH by adding this line: `export PATH=~/.oc:$PATH`
```
vi ~/.bash_profile
```

* Restart terminal for changes to take effect

#### Install Docker
* For Windows Home:
  * Run Docker Toolbox installer
  * Click the Docker Quickstart button after installing, this will start the docker daemon

* For Windows Pro/Enterprise:
  * Run Docker for Windows installer
  * Click on Docker for Windows to start up the docker daemon (a little white whale icon will appear in the bottom bar)
  * Run `~/.oc cluster up` or `oc cluster up` in Git Bash

* Will need to add an insecure registry for oc cluster up to work:
```
vi ~/.docker/machine/machines/docker/config.json
```
  * Add “172.30.0.0/16” to insecure-registries array
  * Run the following to update docker daemon
```
docker-machine provision default
```

#### Run Openshift
  * Run the commands to start the cluster
  ```
~/.oc cluster up
  ```
  **OR**
 ```
oc cluster up
```
