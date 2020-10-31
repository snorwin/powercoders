# Exercise 1 - Pods
The goal of this exercise is to run our first application, an Apache HTTP Server, in OpenShift.
For this we use a `Pod` which is the smallest deployable unit of computing that you can create 
and manage in OpenShift. A `Pod` is a group of one or more containers. In this exercise, we will
deploy a `Pod` that runs a single container with the image `rhscl/httpd-24-rhel7:latest`.

!!! note
    For each exercise you can choose and only have to do either the 'Web Console' or the 'Command Line 
    Interface (CLI)' section in oder to complete the exercise.

=== "Web Console"
    ### Create a `Pod`
    TODO
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: httpd
    spec:
      containers:
      - name: httpd-24
        image: rhscl/httpd-24-rhel7:latest
    ```
    
    ### Inspect a `Pod`
    TODO
    
    ### Delete a `Pod`
    TODO

=== "Command Line Interface (CLI)"
    !!! important
        At the beginning of the exercise make sure that you are in your project context. 
        ```
        oc project <project name> 
        ```
        (replace `<projet name>` with the actual name of your own project)

    ### Create a `Pod`
    1. Create a `Pod` definition file called `pod.yaml` using the [`vi` editor](/powercoders/vieditor/) with the following content:
        ```yaml
        apiVersion: v1
        kind: Pod
        metadata:
          name: httpd
        spec:
          containers:
          - name: httpd-24
            image: rhscl/httpd-24-rhel7:latest
        ```
       _More detailed information about the `Pod` definition file  can be found in the
       [OpenShift](https://docs.openshift.com/container-platform/4.5/nodes/pods/nodes-pods-using.html#nodes-pods-using-example_nodes-pods-using-ssy) or [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/) Documentation._
       
    2. Create a `Pod` by using the `oc apply` command.
        ```
        oc apply -f pod.yaml
        ```
        The output of the command should look like this:
        ```
        [~] $ oc apply -f pod.yaml
        pod/httpd created
        ```
    
    ### Inspect a `Pod`
    1. Let's verify the state of the `Pod` that you have created using `oc get`.
        ```
        oc get pods 
        ```
        You can choose the output format `<output format>` with the `-o` flag. 
        Try some of the formats: `wide`, `json`, `yaml`
        ```
        oc get pods -o <output format>
        ```
    2. `oc describe` can be used to get detailed description of a given resource. 
        Inspect the information and events of your `Pod`.
        ```
        oc descirbe pod <pod name>
        ```
    3.  Print the logs for a container in a `Pod` using the `oc logs` command
        in order to check if the application in the `Pod` was started successfully.
        ```
        oc logs <pod name>
        ```
    4. Also check the 'Inspect a Pod' section for the Web Console.
    
    ### Delete a `Pod`
    1. You won't need the `Pod` in the following exercises, therefore clean up your project.
        ```
        oc delete pod <pod name>
        ```