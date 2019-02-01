# Openshift_Fun

## Q1. 
```
oc new-project q1
oc new-app https://github.com/sclorg/nodejs-ex
```

## Q2.
```
oc new-project q2
oc import-image nodejs --confirm  --from openshift/nodejs-010-centos7
oc new-app -i nodejs https://github.com/sclorg/nodejs-ex
```

## Q3.
```
oc new-project q3
oc create configmap q3-config --from-file=cmapq3.properties
oc create -f q3pod.yaml
oc logs q3
```

Source: https://docs.openshift.com/container-platform/3.11/dev_guide/configmaps.html

## Q4.

```
oc new-project q4
oc create -f q4dc.yaml
oc create secret generic q4secret     --from-literal username=kbaig     --from-literal password=funpass
oc set env dc/q4   --from secret/q4secret
oc logs q4-2-rjpxv
```

## Q5.

```
oc new-project q5
oc create -f q5-pod.yaml
oc logs -f q5
```

## Q6.

```
oc new-project q6
oc create -f q6-pod.yaml
oc logs -f q6
```

## Q7.

```
oc new-project q7
oc create -f q7-pod.yaml
oc logs -f q7
oc create -f q7-service.yaml
# Checked it using redis-cli -h 172.30.32.223 -p 31113 
```

## Q8.

```
oc new-project q8
oc new-app cakephp-mysql-persistent
oc logs -f bc/cakephp-mysql-persistent
oc export all --as-template=cakefun > fun.yaml
```

## Q9.

```
oc new-project q9
oc create -f q9job.yaml
```
