# Introductory Guide to Deploying on OpenShift
OpenShift is a cloud application development platform for container-based software deployment and management, built around a core of application containers powered by Docker and orchestrated by Kubernetes. This quickstart guide will show you how to build and deploy a seed application on an instance of OpenShift.

### Seed Applications
We've created several seed applications to help you get started building applications on OpenShift. Feel free to start from one of these or create your own!
* [Java](https://github.com/rynefagin/java-seed-ghc)
* [Angular](https://github.com/ematusov/ghc-angular-seed)
* [Python 3.5](https://github.com/eleanordare/flask-python-openshift)

You can fork these repos to your own GitHub account by clicking "Fork" in the upper right-hand corner. To work on the applications locally, copy the link under "Clone or Download" and run `git clone <link>` in Terminal on your computer.

### Logging onto OpenShift locally
If you ran `oc cluster up` successfully, you should see the following:

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

> Please see the [installation instructions](https://github.com/eleanordare/red-hat-osd-2017/blob/master/install.md) if `oc cluster up` was not successful.

In your browser, go to `https://127.0.0.1:8443` to see your local instance of OpenShift running. You can log in with username **developer** and any random password.

In Terminal, login with `oc login -u system:admin` to get full cluster-admin access to everything in your OpenShift cluster.

###### Basic OpenShift Commands
* `oc status`
  * see an overview of the current status of your cluster
* `oc get all`
  * get every object in all of your projects
* `oc get pods -n <project>`
  * replace <project> with your project name
  * get all pods from that project
* `oc logs -f bc <app-name> -n <project>`
  * replace <app-name> with your application and <project> with your project name
  * follow the logs of your application as it's building


#### Building and Deploying an Application on OpenShift

1. Navigate to the welcome page of your OpenShift web console and click New Project to create your first project. Give your project any name you like. You can leave Display Name and Description blank.

2. You’ll be taken to a page of templates. Each of these options provides you with a quick setup of all the necessary OpenShift objects for your application:
  * A **build configuration** that defines a build strategy for your application source code to be built into an image. The language you choose on the template page will decide the base image and build strategy for your application.
  * An **image stream** to hold each new built image.
  * A **service** object that contains information about which ports should be exposed and load-balances between your deployed application containers.
  * A **deployment configuration** to define your application’s deployment strategy, the number of pod replicas, container health checks, and what physical resources will be allocated for each pod.
  * A **route** to expose your application service at a host name.

  All you have to do is name your application, choose the correct language/version (i.e. click JavaScript and then the right Node.js version for an AngularJS app, click Python and then the right Python version for a Python app, etc.), and add a Git repo of your source code. OpenShift will handle the rest!

3. *[optional]* Add a webhook trigger to your Git repo with the URL on the next page. In GitHub, go to your repo, then Settings > Webhooks & services. This will kick off a build in OpenShift with your updated code every time you push to Git.

4. View your seed application as it builds by clicking on **Builds** in the sidebar. Click on the **last build** link to see the most recent build, then **Logs** to see the build logs.

5. Once the build has completed, the application’s ImageStream will have been updated with a new image. The DeployConfig contains an “image change trigger” that kicks off a new deployment every time an image is added to the ImageStream. You can see your application deploy by clicking on **Applications > Deployments**, then the last version link to see the most recent deployment.

6. If you scroll down, you’ll see the running pod(s) containing your application. Click on a pod, then **Logs**, to view the application logs as they run in your container.

7. Go to the **Overview** page to see an aggregated view of your project. Click on the large URL above all of the application components and you’ll see your deployed application!

