Mock Exam - 1
--------------
**Question 1:**
Deploy a pod named nginx-pod using the nginx:alpine image.


Once done, click on the Next Question button in the top right corner of this panel. You may navigate back and forth freely between all questions. Once done with all questions, click on End Exam. Your work will be validated at the end and score shown. Good Luck!

Name: nginx-pod
Image: nginx:alpine

**Solution:
Use the command: kubectl run nginx-pod --image=nginx:alpine**

**Question 2:**
Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.

Pod Name: messaging
Image: redis:alpine
Labels: tier=msg

**Solution: Use the command kubectl run messaging --image=redis:alpine -l tier=msg**

**Question 3:**
Create a namespace named apx-x9984574.
Namespace: apx-x9984574

**Solution: Run the command: kubectl create namespace apx-x9984574**

**Question 4:**
Get the list of nodes in JSON format and store it in a file at /opt/outputs/nodes-z3444kd9.json.

**Solution: Run the command: kubectl get nodes -o json > /opt/outputs/nodes-z3444kd9.json**

**Question 5:**
Create a service messaging-service to expose the messaging application within the cluster on port 6379.

Use imperative commands.
Service: messaging-service
Port: 6379
Type: ClusterIp
Use the right labels

**Solution:
Run the command: kubectl expose pod messaging --port=6379 --name messaging-service**

**Question 6:**
Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas.


Name: hr-web-app
Image: kodekloud/webapp-color
Replicas: 2

**Solution: Run the command: kubectl create deployment hr-web-app --image=kodekloud/webapp-color --replicas=2**

**Question 7:**
Create a static pod named static-busybox on the controlplane node that uses the busybox image and the command sleep 1000.

Name: static-busybox
Image: busybox

**Solution: Create a pod definition file in the manifests directory. For that use command kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -oyaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml**

**Question 8:**
Create a POD in the finance namespace named temp-bus with the image redis:alpine.

Name: temp-bus
Image Name: redis:alpine

**Solution: Run the command: kubectl run temp-bus --image=redis:alpine --namespace=finance --restart=Never**

**Question 9:**
A new application orange is deployed. There is something wrong with it. Identify and fix the issue.

**Solution:**
To know more details of orange pod:

**kubectl describe po orange**
and look under the initContainers section. There is an issue with the given command.


**Command:
sh
-c
sleeeep 2;**


In the above, we need to correct the sleeeep command.

To update the pod with an easiest way by running command:

**kubectl edit po orange**
It's not possible to update the changes in the running pod so after saving the changes. It will create a temporary file in the default location /tmp/.

Use that manifest file and replace with the existing pod:

**kubectl replace -f /tmp/kubectl-edit-xxxx.yaml --force**
Above command will delete the existing pod and will recreate the new pod with latest changes.

**Question 10:**
Expose the hr-web-app as service hr-web-app-service application on port 30082 on the nodes on the cluster.


The web application listens on port 8080.

Name: hr-web-app-service
Type: NodePort
Endpoints: 2
Port: 8080
NodePort: 30082

**Solution:**
Run the command: **kubectl expose deployment hr-web-app --type=NodePort --port=8080 --name=hr-web-app-service --dry-run=client -o yaml > hr-web-app-service.yaml** to generate a service definition file.

Now, in generated service definition file add the nodePort field with the given port number under the ports section and create a service.

**Question 11:**
Use JSON PATH query to retrieve the osImages of all the nodes and store it in a file /opt/outputs/nodes_os_x43kj56.txt.

**Solution:**
**Run the command: kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}' > /opt/outputs/nodes_os_x43kj56.txt**

The osImages are under the nodeInfo section under status of each node.

**Question 12:**
Create a Persistent Volume with the given specification: -

Volume name: pv-analytics
Storage: 100Mi
Access mode: ReadWriteMany
Host path: /pv/data-analytics

Solution manifest file to create a persistent volume pv-analytics as follows:

---
apiVersion: v1
kind: PersistentVolume
metadata:
name: pv-analytics
spec:
  capacity:
    storage: 100Mi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteMany
  hostPath:
    path: /pv/data-analytics

