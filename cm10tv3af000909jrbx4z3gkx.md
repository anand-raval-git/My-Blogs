---
title: "Day 36 Task: Managing Persistent Volumes in Your Deployment 💥"
seoTitle: "Managing Persistent Volumes in Deployments"
seoDescription: "Learn to manage Kubernetes Persistent Volumes for your todo app: create PV/PVC, update deployments, verify data access"
datePublished: Fri Sep 13 2024 14:42:31 GMT+0000 (Coordinated Universal Time)
cuid: cm10tv3af000909jrbx4z3gkx
slug: day-36-task-managing-persistent-volumes-in-your-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726294765042/98130dcc-729a-4ee8-8625-d9eb8242d4f8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1726238531622/ee030e3c-217e-4944-9f9d-8daec4d0a359.png
tags: kubernetes, devops, minikube, 90daysofdevops, trainwithshubham

---

## What are Persistent Volumes in k8s

In Kubernetes, a Persistent Volume (PV) is a piece of storage in the cluster that has been provisioned by an administrator. A Persistent Volume Claim (PVC) is a request for storage by a user. The PVC references the PV, and the PV is bound to a specific node. Read official documentation of [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/).

## Today's tasks:

### Task 1:

Add a Persistent Volume to your Deployment todo app.

* Create a Persistent Volume using a file on your node.
    
* Create a Persistent Volume Claim that references the Persistent Volume.
    
* Update your deployment.yml file to include the Persistent Volume Claim. After Applying pv.yml pvc.yml your deployment file look like this
    
* Apply the updated deployment using the command: `kubectl apply -f deployment.yml`
    
* Verify that the Persistent Volume has been added to your Deployment by checking the status of the Pods and Persistent Volumes in your cluster. Use this commands `kubectl get pods` ,
    

`kubectl get pv`

⚠️ Don't forget: To apply changes or create files in your Kubernetes deployments, each file must be applied separately. ⚠️

### Task 2:

Accessing data in the Persistent Volume,

* Connect to a Pod in your Deployment using command : \`kubectl exec -it -- /bin/bash
    

\`

* Verify that you can access the data stored in the Persistent Volume from within the Pod
    

### Let’s do task 1

1. **Create a pv. yml Persistent Volume using a file on your node.**
    
    ```bash
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-app
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      storageClassName: manual
      hostPath:
        path: "/tmp/data"
    ```
    
    * `apiVersion: v1`: Specifies the API version used to create the object.
        
    * `kind: PersistentVolume`: Declares that this is a PersistentVolume (PV), which provides storage to pods.
        
    * `metadata: name: pv-app`: Names the PV as "pv-app".
        
    * `spec:`: Contains the specifications of the PV.
        
        * `capacity`: Defines the storage capacity (not shown fully here, but typically like `storage: 1Gi`).
            
        * `accessModes: - ReadWriteOnce`: Allows the volume to be mounted as read-write by a single node.
            
        * `persistentVolumeReclaimPolicy: Retain`: Prevents data deletion after the PV is released.
            
        * `hostPath: path: "/tmp/data"`: Uses a directory from the host as storage.
            
    
    This configuration sets up a local storage volume with 1GB capacity that can be used by one pod at a time and retains data after release.
    
2. Apply the Persistent Volume:
    
    ```bash
     kubectl apply -f pv.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726162253236/65d10fab-8523-4bab-82a4-9476b60b6210.png align="center")
    
3. **Create a pvc.yml Persistent Volume Claim that references the Persistent Volume.**
    
    ```bash
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-app
      namespace: app-deployment
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
      storageClassName: manual
    ```
    
    * `apiVersion: v1`: Specifies the API version for the resource. `v1` is the stable version for core Kubernetes resources like PV and PVC.
        
    * `kind: PersistentVolume`: Indicates that this is a `PersistentVolume` resource. A `PersistentVolume` is a piece of storage in the cluster that has been provisioned by an administrator.
        
    * `metadata`:
        
        * `name: pvc-app`: A name for this `PersistentVolume`. It’s used to identify the resource in the Kubernetes cluster.
            
    * `spec`:
        
        * `accessModes`:
            
            * `- ReadWriteOnce`: Specifies the access modes for the `PersistentVolume`. `ReadWriteOnce` means the volume can be mounted as read-write by a single node.
                
        * `resources`:
            
            * `requests`:
                
                * `storage: 500Mi`: Specifies the amount of storage requested. However, this field is used in `PersistentVolumeClaim`, not in `PersistentVolume`. For `PersistentVolume`, you should define the `capacity` field instead.
                    
4. Apply the Persistent Volume Claim:
    
    ```bash
     kubectl apply -f pvc.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726162707461/94388c31-6a40-49d3-a637-22fead2d2349.png align="center")
    
5. Create file name called storageclass.yml
    
    ```bash
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: manual
    provisioner: k8s.io/minikube-hostpath  # This is for local testing; adjust as needed for your environment
    ```
    
    ### `provisioner:` [`k8s.io/minikube-hostpath`](http://k8s.io/minikube-hostpath)
    
    The `provisioner` field specifies which provisioner will be responsible for creating and managing Persistent Volumes (PVs).
    
    * [`k8s.io/minikube-hostpath`](http://k8s.io/minikube-hostpath) is a provisioner used for **Minikube**, a Kubernetes environment designed for local testing. The `hostPath` provisioner stores data directly on the host node's filesystem, which is useful in development and testing scenarios but not recommended for production environments.
        
    
    ### Use Case
    
    This StorageClass is likely meant for local development and testing using Minikube. When a **PersistentVolumeClaim (PVC)** is created and uses this StorageClass, Kubernetes will use the `hostPath` provisioner to create storage directly on the local machine where Minikube is running.
    
    In production environments, you would use different provisioners (like `aws-ebs` for AWS, `gce-pd` for GCP, etc.), depending on the cloud platform or storage solution you're using.
    
    ```bash
    kubectl apply -f storageclass.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726235394877/cd79d4a9-e3ed-4672-9203-1126ffc9c5fa.png align="center")
    
6. **Let’s update deployment file so create new update\_deployment\_3.0.yml file to include the Persistent Volume Claim.**
    
    ```bash
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: django-todo-deployment
      namespace: app-deployment
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: django-todo
      template:
        metadata:
          labels:
            app: django-todo
        spec:
          containers:
          - name: django-todo
            image: anandraval12/django-todo-app:latest
            ports:
            - containerPort: 8000
            env:
            - name: DATABASE_URL
              valueFrom:
                secretKeyRef:
                  name: django-secret
                  key: database-url
            - name: SECRET_KEY
              valueFrom:
                secretKeyRef:
                  name: django-secret
                  key: secret-key
            volumeMounts:
            - name: todo-data
              mountPath: /app
          volumes:
          - name: todo-data
            persistentVolumeClaim:
              claimName: pvc-app
    ```
    
7. Apply the updated deployment:
    
    ```bash
     kubectl apply -f deployment.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726163615909/87e51abe-5680-4744-8daa-5277bd7f6be3.png align="center")
    
8. **Verify the Persistent Volume has been added to your Deployment.**
    
    ```bash
     kubectl get pods -n <name-space name>
     kubectl get pv
     kubectl get pvc
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726164482683/d012496c-9c18-4aa4-bd37-816f9a8b7373.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726164524735/b05a3bdb-6383-4b7a-aa1c-ea8a9e252a0e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726164542630/30221304-909e-4f39-9ed4-ccc6153fe4bb.png align="center")

### Let’s do task 2

1. **Get the Pod details:**
    
    ```bash
     kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726164570051/08c3e80e-7205-4c5a-b3cc-605369feadd1.png align="center")
    
2. **Connect to a Pod in your Deployment:**
    
    ```bash
     kubectl exec -it <pod-name> -- /bin/bash
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726236954725/0c25a899-4665-4290-be7f-f3f401456bfd.png align="center")
    
3. **Verify that you can access the data stored in the Persistent Volume from within the Pod:**
    
    ```bash
     cd /app/
     echo "Hello" > /app/test.txt
     ls
    ```
    
4. **Delete the pod and verify the data persistence:**
    
    ```bash
     kubectl delete pod <pod-name>
     kubectl get pods
     kubectl exec -it <new-pod-name> -- /bin/bash
     cd /app/
     ls
     cat test.txt
    ```
    
    Thankyou for reading !!!!!!