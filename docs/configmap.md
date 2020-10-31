# Exercise 4 - ConfigMaps

We want to change the `index.html` served by the Apache HTTP Server in order to personalize our website.
There are multiple approaches to achieve this:

- change the container image by adding the file during the build to the image (out of scope for this workshop)
- use a `ConfigMap` to inject the file to the container in the `Pod`

`ConfigMap` provides a mechanisms to inject containers with configuration data (entire files or single values) while keeping the containers unchanged. 

_Check out the [OpenShift](https://docs.openshift.com/container-platform/4.5/builds/builds-configmaps.html) or [Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/) Documentation for more information about `ConfigMaps`._

!!! note
    For each exercise you can choose and only have to do either the 'Web Console' or the 'Command Line 
    Interface (CLI)' section in oder to complete the exercise.

=== "Web Console"
    ### Create a `ConfigMap`

    ### Inspect a `ConfigMap`

    ### Mount a `ConfigMap`

=== "Command Line Interface (CLI)"
    !!! important
        At the beginning of the exercise make sure that you are in your project context. 
        ```
        oc project <project name> 
        ```

    ### Create a `ConfigMap`
    1. Create a `index.html` file using the [`vi` editor](/vieditor/#vi-editor) with the following content:
        ```
        <!DOCTYPE html>
        <html>
        <head>
            <title>John Doe</title>
        </head>
        <body>
            <h1>John Doe</h1>
            <p>
            Today I learned how to deploy my own website in the cloud
            using an Apache HTTP Server (httpd) running on OpenShift.
            </p>
        </body>
        </html>
        ```
        (replace `John Doe` with your actual name - if you are John Doe you can skip this)
    2. Create a `ConfigMap` with the `index.html`.
        ```
        oc create configmap httpd --from-file=index.html
        ```
    
    ### Inspect a `ConfigMap`
    1. Inspect the created `ConfigMap` using `oc get` and `oc describe`.
        ```
        oc get configmaps
        oc describe configmap <configmap name>
        ```
    2. Also check the 'Inspect a ConfigMap' section for the Web Console.

    ### Mount a `ConfigMap`
    1. Let's add the `ConfigMap` to the `Pod` template in the `Deployment`.
        The `oc edit` command allows us to edit existing resources using the [`vi` editor](/vieditor/#vi-editor).
        ```
        oc edit deployment <deployment name>
        ```
    2. Add the ==higlighted== parts to the `Deployment`:
        ``` hl_lines="5 6 7 8 12 13 14"
        apiVersion: apps/v1
        kind: Deployment
        ...
        spec:
          volumes:
          - name: html
            configMap:
              name: <configmap name> 
          ...
          containers:
          - image: rhscl/httpd-24-rhel7:latest
            volumeMounts:
            - name: html
              mountPath: /var/www/html
            ...
        ```
    3. Store and close the file.
        The configuration change triggers automatically a redeployment of all your `Pods` - wait a couple of seconds until it is done.
    4. Reload your web site using the URL of the `Route` created in [Exercise 3](/networking).


### **🎉 Congratulations, you have made it!**
You have successfully deployed your first personal website in the cloud using OpenShift. 👏