## Kubernetes Debugging Exercise

For this exercise, I used the Helm chart from the last task. I modified the `command` and `args` of the nginx container to run a deliberate `systemctl` command. As a result, the container was not able to start successfully.

After deploying the application, I checked the status of the pods with `kubectl get pods` and noticed that they were not running. I then performed the following steps to identify the issue:

1. **Checked for image pull issues**  
   First, I ruled out any network problems between the container registry and the node, which could cause an image pull error.

2. **Verified pod scheduling**  
   Next, I checked whether the pods were successfully scheduled to rule out resource constraints or taint-related issues:
   ```bash
   kubectl describe po/<pod-name>

3. **Checked pod logs (default container)**
    After ruling out resource issues, I examined the logs of the pod:
    ```bash
    kubectl logs <pod-name>

    This showed logs from another container running in the same pod.

4. **Checked logs of the nginx container**
    Finally, I checked the logs specifically for the nginx container:
    ```bash
    kubectl logs <pod-name> -c nginx

    At this point, I discovered that the systemctl command was not available in the container. Therefore, the nginx container failed to start.