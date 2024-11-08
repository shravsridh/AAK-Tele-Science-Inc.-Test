# AAK-Tele-Science-Inc.-Test

For this task, I assumed that the cluster nodes A, B, and C are already created.

### Overview of the YAML files:

**1. Node labelling:** These files are to label the cluster nodes so that the correct Nginx deployment pod can be scheduled on the corresponding node, using the label.<br/><br/>
   a. _node-A-labelling.yaml:_ File to label node A<br/>
   b. _node-B-labelling.yaml:_ File to label node B<br/>
   c. _node-C-labelling.yaml:_ File to label node C<br/>

**2. Configuration for Nginx deployments for the pods:** These files are to specify configurations for the Nginx deployments for the 3 pods, F, T, and J.<br/><br/>
   a. _deployment-pod-nginx-F.yaml:_ File to specify configuration for Nginx deployment for pod F<br/>
   b. _deployment-pod-nginx-T.yaml:_ File to specify configuration for Nginx deployment for pod T<br/>
   c. _deployment-pod-nginx-J.yaml:_ File to specify configuration for Nginx deployment for pod J<br/>

### If we execute the following commands in the appropriate runtime environment, the scheduling operations required as per the task should be performed:

1. Check that the 3 cluster nodes A, B, and C exist.
   
   ```
   kubectl get nodes
   ```

2. Apply the node labels (and taint for node C) by applying the corresponding YAML files.

   ```
   kubectl apply -f node-A-labelling.yaml
   kubectl apply -f node-B-labelling.yaml
   kubectl apply -f node-C-labelling.yaml
   ```

3. Check that the labels were correctly applied.

   ```
   kubectl get nodes --show-labels
   ```

   OR

   ```
   kubectl describe node nodeA
   kubectl describe node nodeB
   kubectl describe node nodeC
   ```

5. Check that the taint (for node C) was correctly applied.

   ```
   kubectl describe nodes | grep Taint
   ```

6. Apply the 3 Nginx deployments by applying the corresponding YAML files.

   ```
   kubectl apply -f deployment-pod-nginx-F.yaml
   kubectl apply -f deployment-pod-nginx-T.yaml
   kubectl apply -f deployment-pod-nginx-J.yaml
   ```

7. Check that the Nginx deployment pods are scheduled on the correct cluster nodes as per the task requirements.

   ```
   kubectl get pods -o wide
   kubectl get pods -l app=nginx_F -o wide
   kubectl get pods -l app=nginx_T -o wide
   kubectl get pods -l app=nginx_J -o wide
   ```
