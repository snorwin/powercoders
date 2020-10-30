# 2 - Deployment

## Web Console

## Command Line Interface (CLI)
### 2.1 - Create a Deployment
1. At the beginning of the exercise make sure that you are in your project context. 
    ```shell script
    oc project <project name> 
    ```
   (replace `<projet name>` with the actual name of your own project)
2. Create a deployment of the using the `oc create` command:
    ```shell script
    oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
    ```
   The output of the command should look this:
   ```
   [~] $ oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
   deployment.apps/httpd created
    ```

### 2.2 - Inspect a Deployment
1. 
   ```shell script
   oc get deployments -o wide
   oc descirbe deployment <deployment name>
   ```

```shell script
oc get pods 
```

```shell script
oc get pods -o wide
```



## Delete a Pod
### Web Console

### Command Line Interface (CLI)
```shell script
oc delete pod <pod name>
```