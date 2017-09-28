Terminology

|Word/Phrase|Definition|
|---|:---|
|Project/Namespace|A mechanism to scope resources inside a cluster. It allows a community of users to organize and manage their content in isolation from other communities, with admin, edit, or view access to OpenShift objects in the project.|
|Image|A binary that includes all of the requirements for running a single container, as well as metadata describing its needs and capabilities. Containers in OCP are based on Docker-formatted container images.|
|Container|Lightweight mechanisms for isolating running processes so that they are limited to interacting with only their designated resources.|
|Pod|One or more containers deployed together on one host. The smallest compute unit that can be defined, deployed, and managed.|
|Services|A service serves as an internal load balancer. It identifies a set of replicated pods in order to proxy the connections it receives to them. Services are assigned an IP address and port pair that proxy to an appropriate backing pod. It uses a label selector to find all the containers running that provide a certain network service on a certain port.|
|Routes|Exposes a service at a hostname so that external clients can reach it by name.|
|Replication Controllers|Ensures that a specified number of replicas of a pod are running at all times.|
|Builds / BuildConfig|A build is the process of transforming input parameters or source code into a runnable image. A build configuration describes a single build definition and a set of triggers for when a new build should be created.|
|Deployments / DeploymentConfig|A deployment creates a new replication controller and lets it start up pods, with additional options in the DeploymentConfig object for transitioning from existing image deployments to new ones.|
|Templates|A set of objects that can be parameterized and processed to produce a list of objects for creation by OCP (ex. Services, build configurations, deployment configurations, etc.).|
|Image Streams|An image stream comprises any number of Docker-formatted container images identified by tags. They can be used to automatically perform an action when new images are created (ex. builds can watch an image stream to receive notifications when new images are added and perform a build).|
