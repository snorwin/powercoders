# Exercise 2 - Deployments



!!! note
    For each exercise you can choose and only have to do either the 'Web Console' or the 'Command Line 
    Interface (CLI)' section in oder to complete the exercise.

=== "Web Console"

=== "Command Line Interface (CLI)"
    !!! important
        At the beginning of the exercise make sure that you are in your project context. 
        ```
        oc project <project name> 
        ```

    ### Create a Deployment
    1. Create a deployment of the Apache HTTP Server using the `oc create` command:
        ```
        oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
        ```
        The output of the command should look this:
        ```
        [~] $ oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
        deployment.apps/httpd created
        ```

    ### Inspect a Deployment
    1. 
        ```
        oc get deployments -o wide
        oc descirbe deployment <deployment name>
        ```
    
        ```
        oc get pods 
        ```
        
        ```
        oc get pods -o wide
        ```
    
    ### Scale a Deployment