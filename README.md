# Openshift_Fun

### Q1. 
```
oc new-project q1
oc new-app https://github.com/sclorg/nodejs-ex
```

### Q2.
```
oc new-project q2
oc import-image nodejs --confirm  --from openshift/nodejs-010-centos7
oc new-app -i nodejs https://github.com/sclorg/nodejs-ex
```

### Q3.
```
oc new-project q3
# Creating configmap
oc create configmap q3-config --from-file=cmapq3.properties
# Creating pods which has configmap mounted. It echo content.
oc create -f q3pod.yaml
oc logs -f q3
```

### Q4.

```
oc new-project q4
oc create -f q4dc.yaml
oc create secret generic q4secret     --from-literal username=kbaig     --from-literal password=funpass
oc set env dc/q4   --from secret/q4secret
oc logs -f q4-2-rjpxv
```

### Q5.

```
oc new-project q5
# Create pod which has init container which download image and then main container give it's sum
# They share the volume
oc create -f q5-pod.yaml
oc logs -f q5
```

### Q6.

```
oc new-project q6
# Create a pod containing containers having non persistence volume
oc create -f q6-pod.yaml
oc logs -f q6
```

### Q7.

```
oc new-project q7
oc create -f q7-pod.yaml
oc logs -f q7
oc create -f q7-service.yaml
# Checked it using redis-cli -h 172.30.32.223 -p 31113 
```

### Q8.

```
oc new-project q8
oc new-app cakephp-mysql-persistent
oc logs -f bc/cakephp-mysql-persistent
oc export all --as-template=cakefun > fun.yaml
```

### Q9.

```
oc new-project q9
oc create -f q9job.yaml
```


### Q10.
Deployment is a collection of one or more pods while pod is a collection of one or more containers. Deployment has ability to heal, fault tolerance, change control and replication whereas pod don't.

### Q11.
#### Build Config
Build config has triggers for when to build, type of source and build strategy which determines how to transform input sources given to a desired build object. Build strategy available are Source, Pipeline, Docker and Custom. Input sources are Git, Dockerfile, Binary, Image, Input Secrets and External artifacts.
#### S2I
S2I has three components for build object: source, s2i scripts and builder image. To build first s2i create tar of script and source which is streamed to builder image. Then s2i untars into the location specified in builder image. If incremental build, then build artifacts are restored. Then assemble script is run to build. If Incremental build, then save-artifacts script saves all artifacts to a tar file. Otherwise, container is committed and CMD of image is set to run script.

### Q12.
Image stream is a pointer to an image stream or images and it's associated tags available either externally or internally. It provides an abstraction over image and saves end user from uncertainity in url. Also, it can be used to configure trigger for deployment.

### Q13.
Liveness probe is a probe that checks the health of application. Liveness probe can be defined using cmd, http or TCP call. If it fails, then application is restarted.
Readiness probe is probe that checks whether application is ready to receive the request. If it fails, then application doesn't receive request from service.
We would use readiness probe if application requires time to load data, fetch data for the application to be ready.
We would use liveness probe to ensure that our app is reliable.
