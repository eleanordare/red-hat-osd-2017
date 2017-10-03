# OpenShift Recently Asked Questions

## Installation / Deployment FAQ

### What Version Should I be installing?

You should be using Docker 1.12 or higher (1.17 preferred) and OpenShift 3.6.0 

### What if my initial build hangs and does not complete?

Check your docker version. This can happen if you're using an outdated version of docker, such as 1.10. You can determine what version of docker you are using by trying 

```
docker --version
```

