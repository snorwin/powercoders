# Exercise 2 - Deployments
You describe the desired state of your application in a `Deployment` by specifying the number of replicas and a `Pod` template.
The `Deployment` involve a `ReplicaSet` to manage the `Pods` in the background.

The `ReplicaSet` ensures that specified number of `Pod` replicas are running all the time.
If a `Pod` crashes or is deleted the `ReplicaSet` creates new instances up to the defined number.
Likewise, if there are more `Pods` running than desired, it deletes as many as necessary.

_Check out the [OpenShift](https://docs.openshift.com/container-platform/4.5/applications/deployments/what-deployments-are.html#deployments-repliasets_what-deployments-are) or [Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) Documentation for more information about `Deployemnts` and `ReplicaSets`._

!!! note
    For each exercise you can choose and only have to do either the 'Web Console' or the 'Command Line 
    Interface (CLI)' section in oder to complete the exercise.

=== "Web Console"
    ### Create a `Deployment`
    TODO

    ### Inspect a `Deployment`
    TODO

    ??? question "What is the difference between the `Pod` that was created manually and the one that was created by the `Deployment`?"
        The `Pod` created from the `Deployment` have a random name.

        _Example:_
        ```
        httpd-12cf4d11ce-p9w5h
        ```
        The `Deployment` adds a random string (e.g. `12cf4d11ce`) to the deployment name while creating the `ReplicaSet`.
        The `ReplicaSet` itself adds  another random string to the each `Pod` (e.g. `p9w5h`).
  
    ??? question "What happens if you delete a pod uisng `oc delete pod <pod name>`?"
        The `ReplicaSet` of the `Deployment` automatically creates a new `Pod`. The same would happen if the application in the container of the `Pod` crashed or terminated.
    
    
    ### Scale a `Deployment`
    TODO

=== "Command Line Interface (CLI)"
    !!! important
        At the beginning of the exercise make sure that you are in your project context. 
        ```
        oc project <project name> 
        ```

    ### Create a `Deployment`
    1. Create a `Deployment` of the Apache HTTP Server using the `oc create` command:
        ```
        oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
        ```
        The output of the command should look this:
        ```
        [~] $ oc create deployment httpd --image rhscl/httpd-24-rhel7:latest
        deployment.apps/httpd created
        ```

    ### Inspect a `Deployment`
    1. Let's verify the state of the `Deployment` that you have created using `oc get` and `oc describe`.
        ```
        oc get deployments -o wide
        oc describe deployment <deployment name>
        ```

    2. Inspect the pods the `Deployment` has created.
        ```
        oc get pods
        oc get pods -o wide
        ```

        ??? question "What is the difference between the `Pod` that was created manually and the one that was created by the `Deployment`?"

            The `Pod` created from the `Deployment` have a random name.

            _Example:_
            ```
            httpd-12cf4d11ce-p9w5h
            ```
            The `Deployment` adds a random string (e.g. `12cf4d11ce`) to the deployment name while creating the `ReplicaSet`.
            The `ReplicaSet` itself adds  another random string to the each `Pod` (e.g. `p9w5h`).

        ??? question "What happens if you delete a pod uisng `oc delete pod <pod name>`?"

            The `ReplicaSet` of the `Deployment` automatically creates a new `Pod`. The same would happen if the application in the container of the `Pod` crashed or terminated.

    3. Also check the 'Inspect a Deployment' section for the Web Console.
    
    ### Scale a `Deployment`
    1. Scale the `Deployment` to have another `Pod` of the application to achieve a redundant and stable setup.
        ```
        oc scale deployment <deployment name> --replicas=2
        ```
    2. Inspect the `Deployment` and pods again.