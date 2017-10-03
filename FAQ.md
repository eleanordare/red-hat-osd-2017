# OpenShift Frequently Asked Questions

## Installation / Deployment FAQ

### What Version Should I be installing?

You should be using Docker 1.12 or higher (17 preferred) and OpenShift 3.6.0 

### What if I am unable to add the oc file to /usr/bin directory?

This step is not necessary in order to make oc work, although it makes things easier. If you are unable to gain root access to add oc to /usr/bin, simply navigate within the openshift-origin-client-tools folder to the directory which contains 'oc'. From there, you can run 

```
oc cluster up 
```

You will have to execute oc from this folder each time, and it will not be accessible from everywhere in your command line.

### What if oc cannot connect to the Docker daemon?

Check to make sure you have restarted the docker service and that it is running. 

```
systemctl status docker
systemctl restart docker
```

### What if my initial build hangs and does not complete?

Check your docker version. This can happen if you're using an outdated version of docker, such as 1.10. You can determine what version of docker you are using by trying 

```
docker --version
```

If you have the wrong version of docker, check to make sure you've set up the right docker repository for docker-ce. If you do not setup the repository, your software package tool (yum, dnf, brew) might pull an outdated version.

### What if the route to my application gives me a 404?

This can happen if the default OpenShift port is set to something different than you have defined in your application.You can check which port your OpenShift application is going to by clicking on **Application > Services** to see which port is exposed. 

To change this, go to your application code and find where you have defined the default route. Change this to match the route that OpenShift goes to.

### If something goes wrong, where can I access the logs?

There are multiple places you can find the logs, though some will have more details than others. In **Applications > Pods > Applicationname-1-...** , you will be able to see the most detailed logs regarding your deployment and runtime. 

