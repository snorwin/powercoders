# Pods

## Create a Pod
### Web Console

### Command Line Interface (CLI)
```shell script
oc porject <project name> 
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: httpd
spec:
  containers:
  - name: httpd-24
    image: rhscl/httpd-24-rhel7:latest
```

```shell script
oc apply -f pod.yaml
```

## Inspect a Pod
### Web Console

### Command Line Interface (CLI)
```shell script
oc get pods 
```

```shell script
oc get pods -o wide
```

```shell script
oc descirbe pod <pod name>
oc logs <pod name>
```

## Delete a Pod
### Web Console

### Command Line Interface (CLI)
```shell script
oc delete pod <pod name>
```