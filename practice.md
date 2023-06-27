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

---
Mock Exam - 2
--------------

**Question : 1**
**Take a backup of the etcd cluster and save it to /opt/etcd-backup.db.**

**Solution:**
Run the following command to take a backup:
**export ETCDCTL_API=3**
**etcdctl snapshot save --endpoints https://[127.0.0.1]:2379 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key  /opt/etcd-backup.db**

**Question 2:**
**Create a Pod called redis-storage with image: redis:alpine with a Volume of type emptyDir that lasts for the life of the Pod.

Specs on the below.
Pod named 'redis-storage' created
Pod 'redis-storage' uses Volume type of emptyDir
Pod 'redis-storage' uses volumeMount with mountPath = /data/redis**

**Solution:**
Use the command kubectl run and create a pod definition file for redis-storage pod and add volume.
Alternatively, run the command:
**kubectl run redis-storage --image=redis:alpine --dry-run=client -oyaml > redis-storage.yaml**
and add volume emptyDir in it.

Solution manifest file to create a pod redis-storage as follows:

![img.png](img.png)

**Question 3:**
**Create a new pod called super-user-pod with image busybox:1.28. Allow the pod to be able to set system_time.

The container should sleep for 4800 seconds.
Pod: super-user-pod
Container Image: busybox:1.28
Is SYS_TIME capability set for the container?**

**Solution:**
Solution manifest file to create a pod super-user-pod as follows:

![img_1.png](img_1.png)

**Question 4:**
**A pod definition file is created at /root/CKA/use-pv.yaml. Make use of this manifest file and mount the persistent volume called pv-1. Ensure the pod is running and the PV is bound.

mountPath: /data
persistentVolumeClaim Name: my-pvc
persistentVolume Claim configured correctly
pod using the correct mountPath
pod using the persistent volume claim?**

**solution:**
Add a persistentVolumeClaim definition to pod definition file.
Solution manifest file to create a pvc my-pvc as follows:

![img_2.png](img_2.png)
![img_3.png](img_3.png)

**Question 5:**
**Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. Next upgrade the deployment to version 1.17 using rolling update.

Deployment : nginx-deploy. Image: nginx:1.16
Image: nginx:1.16
Task: Upgrade the version of the deployment to 1:17
Task: Record the changes for the image upgrade**

**Solution:**

Explore the --record option while creating the deployment while working with the deployment definition file. Then make use of the kubectl apply command to create or update the deployment.

To create a deployment definition file nginx-deploy:

**kubectl create deployment nginx-deploy --image=nginx:1.16 --dry-run=client -o yaml > deploy.yaml**
To create a resource from definition file and to record:

**kubectl apply -f deploy.yaml --record**
To view the history of deployment nginx-deploy:

**kubectl rollout history deployment nginx-deploy**
To upgrade the image to next given version:

**kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record**
To view the history of deployment nginx-deploy:

**kubectl rollout history deployment nginx-deploy**

**Question 6:**
**Create a new user called john. Grant him access to the cluster. John should have permission to create, list, get, update and delete pods in the development namespace . The private key exists in the location: /root/CKA/john.key and csr at /root/CKA/john.csr.

Important Note: As of kubernetes 1.19, the CertificateSigningRequest object expects a signerName.
Please refer the documentation to see an example. The documentation tab is available at the top right of terminal.
CSR: john-developer Status:Approved
Role Name: developer, namespace: development, Resource: Pods
Access: User 'john' has appropriate permissions**

**Solution:**
![img_4.png](img_4.png)
**kubectl create role developer --resource=pods --verb=create,list,get,update,delete --namespace=development**
**kubectl create rolebinding developer-role-binding --role=developer --user=john --namespace=development**
To verify the permission from kubectl utility tool:
**kubectl auth can-i update pods --as=john --names**

**Question 7:**
**Create a nginx pod called nginx-resolver using image nginx, expose it internally with a service called nginx-resolver-service. Test that you are able to look up the service and pod names from within the cluster. Use the image: busybox:1.28 for dns lookup. Record results in /root/CKA/nginx.svc and /root/CKA/nginx.pod

Pod: nginx-resolver created
Service DNS Resolution recorded correctly
Pod DNS resolution recorded correctly**

**Solution:**
Use the command kubectl run and create a nginx pod and busybox pod. Resolve it, nginx service and its pod name from busybox pod.

To create a pod nginx-resolver and expose it internally:

**kubectl run nginx-resolver --image=nginx
kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP**
To create a pod test-nslookup. Test that you are able to look up the service and pod names from within the cluster:

**kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service > /root/CKA/nginx.svc**
Get the IP of the nginx-resolver pod and replace the dots(.) with hyphon(-) which will be used below.

**kubectl get pod nginx-resolver -o wide
kubectl run test-nslookup --image=busybox:1.28 --rm**

**Question 8:**
**Create a static pod on node01 called nginx-critical with image nginx and make sure that it is recreated/restarted automatically in case of a failure.

Use /etc/kubernetes/manifests as the Static Pod path for example.
static pod configured under /etc/kubernetes/manifests ?
Pod nginx-critical-node01 is up and running**

**Solution:**
To create a static pod called nginx-critical by using below command:

**kubectl run nginx-critical --image=nginx --dry-run=client -o yaml > static.yaml**
Copy the contents of this file or use scp command to transfer this file from controlplane to node01 node.

**root@controlplane:~# scp static.yaml node01:/root/**
To know the IP Address of the node01 node:

**root@controlplane:~# kubectl get nodes -o wide**

# Perform SSH
**root@controlplane:~# ssh node01
OR
root@controlplane:~# ssh <IP of node01>
On node01 node:**

Check if static pod directory is present which is /etc/kubernetes/manifests, if it's not present then create it.

**root@node01:~# mkdir -p /etc/kubernetes/manifests**
Add that complete path to the staticPodPath field in the kubelet config.yaml file.

**root@node01:~# vi /var/lib/kubelet/config.yaml**
now, move/copy the static.yaml to path /etc/kubernetes/manifests/.

**root@node01:~# cp /root/static.yaml /etc/kubernetes/manifests/**
Go back to the controlplane node and check the status of static pod:

**root@node01:~# exit
logout
root@controlplane:~# kubectl get pods** 