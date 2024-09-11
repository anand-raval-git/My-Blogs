---
title: "Day 35: Mastering ConfigMaps and Secrets in Kubernetes🔒🔑🛡️"
seoTitle: "Master ConfigMaps & Secrets in Kubernetes"
seoDescription: "Learn to create and manage ConfigMaps and Secrets in Kubernetes, ensuring secure and efficient configuration management in your deployments"
datePublished: Wed Sep 11 2024 15:55:28 GMT+0000 (Coordinated Universal Time)
cuid: cm0y1l6sh00060ajnb6sebtif
slug: day-35-mastering-configmaps-and-secrets-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726070077895/4972ae8e-b261-4a0d-aff4-4fc78fe70010.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1726070106851/e0287c03-1c25-4d50-a4bb-c4540a7db6ba.png
tags: kubernetes, devops, minikube, 90daysofdevops, trainwithshubham

---

### 👏🎉 Yay! Yesterday we conquered Namespaces and Services 💪💻🔗🚀

## What are ConfigMaps and Secrets in k8s

In Kubernetes, ConfigMaps and Secrets are used to store configuration data and secrets, respectively. ConfigMaps store configuration data as key-value pairs, while Secrets store sensitive data in an encrypted form.

* *Example :- Imagine you're in charge of a big spaceship (Kubernetes cluster) with lots of different parts (containers) that need information to function properly. ConfigMaps are like a file cabinet where you store all the information each part needs in simple, labeled folders (key-value pairs). Secrets, on the other hand, are like a safe where you keep the important, sensitive information that shouldn't be accessible to just anyone (encrypted data). So, using ConfigMaps and Secrets, you can ensure each part of your spaceship (Kubernetes cluster) has the information it needs to work properly and keep sensitive information secure! 🚀*
    
* Read more about [ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/) & [Secret](https://kubernetes.io/docs/concepts/configuration/secret/).
    

## Today's task:

## Task 1:

* Create a ConfigMap for your Deployment
    
* Create a ConfigMap for your Deployment using a file or the command line
    
* Update the deployment.yml file to include the ConfigMap
    
* Apply the updated deployment using the command: `kubectl apply -f deployment.yml -n <namespace-name>`
    

Verify that the ConfigMap has been created by checking the status of the ConfigMaps in your Namespace.

### Let’s do task 1

1. **create a configMap.yml file**
    
    ```bash
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: django-config
      namespace: app-deployment
    data:
      name: django-app
      application: todo-app
      protocol: TCP
    ```
    

### Explanation:

1. `apiVersion: v1`
    
    * Specifies the version of the Kubernetes API used for this ConfigMap. For ConfigMaps, it's always `v1`.
        
2. `kind: ConfigMap`
    
    * Indicates the type of Kubernetes resource. In this case, it's a `ConfigMap`.
        
3. `metadata:`
    
    * Contains metadata about the ConfigMap.
        
    * `name: django-config`: This is the unique name of the ConfigMap within the specified namespace. In this case, it's called `django-config`.
        
    * `namespace: app-deployment`: This specifies the namespace where the ConfigMap is created. If you don’t specify a namespace, it defaults to `default`.
        
4. `data:`
    
    * This section contains the actual configuration data stored in the ConfigMap.
        
    * `name: django-app`: A key-value pair where the key is `name` and the value is `django-app`. This can be used by applications or pods to access this value.
        
    * `application: todo-app`: Another key-value pair where `application` is the key and `todo-app` is the value.
        
    * `protocol: TCP`: A key-value pair where `protocol` is the key and `TCP` is the value.
        

Now create the ConfigMap by running the following command:

```bash
kubectl apply -f configmap.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726067207396/886c0014-329a-4256-93f3-c29d1d054d07.png align="center")

**Now create update\_deployment.yaml file to include the ConfigMap**

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
          - name: application
            valueFrom:
              configMapKeyRef:
                name: django-config
                key: application
```

`env:`

* `- name: application`: Specifies the name of the environment variable to set inside the container.
    
* `valueFrom:`
    
    * `configMapKeyRef:`: Refers to a key in a ConfigMap to set the value of the environment variable.
        
        * `name: django-config`: The name of the ConfigMap from which to retrieve the value.
            
        * `key: application`: The key in the ConfigMap whose value will be assigned to the environment variable `application`
            

the pod definition includes an environment variable application whose value is taken from the ConfigMap. The **valueFrom** field specifies the source of the value, which is the ConfigMap **my-config-map** and the key application.

**Now Apply the updated deployment using the below command**

```bash
kubectl apply -f deployment.yaml 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726067714746/372f2d80-77d0-4dab-ac2c-a9bb20231790.png align="center")

**Let’s Verify that the ConfigMap has been created by checking the status of the ConfigMaps in your Namespace.**

To verify that the ConfigMap has been created, you can use the following command:

```bash
kubectl get configmap 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726067978630/02f968cc-cc5b-473c-acba-11ee6d3ec80d.png align="center")

You can also use the following command to view the details of a specific ConfigMap:

This command will display detailed information about the ConfigMap, including its metadata, data, and status.

```bash
kubectl describe configmap 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726068040712/889afea6-cf24-4330-a2ef-8991bec0f393.png align="center")

To see the key-value pairs of an environment variable in a ConfigMap inside a cluster or a pod, you can use the following command:

```bash
kubectl exec -it <pod-name> -- bash
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726068113149/65589d03-4192-47c2-8cd3-db8579efad30.png align="center")

Once inside the pod, you can use the following command to see the value of an environment variable:

```bash
echo $key-name
```

You can also use the following command to see all the environment variables defined in the pod:

```bash
printenv
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726068201738/63e320d4-bef8-48c5-b639-acc701f4073f.png align="center")

In above example, key is application and value of that key is todo-app.

## Task 2:

* Create a Secret for your Deployment
    
* Create a Secret for your Deployment using a file or the command line
    
* Update the deployment.yml file to include the Secret
    
* Apply the updated deployment using the command: `kubectl apply -f deployment.yml -n <namespace-name>`
    
* Verify that the Secret has been created by checking the status of the Secrets in your Namespace.
    

### **Let’s do task 2**

1. create a secret.yml file
    
    ```bash
    apiVersion: v1
    kind: Secret
    metadata:
      name: django-secret
      namespace: app-deployment
    type: Opaque
    data:
      database-url: dXNlcjpwYXNzd29yZA== # base64-encoded value of 'user:password'
      secret-key: QW5hbmQgUmF2YWw=  # base64-encoded value of 'Anand Raval'
    ```
    

### Explanation:

1. `apiVersion: v1`
    
    * Specifies the version of the Kubernetes API used for the Secret resource. For Secrets, it is `v1`.
        
2. `kind: Secret`
    
    * Indicates the type of Kubernetes resource. In this case, it's a `Secret`.
        
3. `metadata:`
    
    * `name: django-secrets`: The name of the Secret object.
        
    * `namespace: app-deployment`: The namespace where the Secret is created.
        
4. `type: Opaque`
    
    * The `type` field specifies the type of Secret. `Opaque` is the default and is used for arbitrary user-defined data.
        
5. `data:`
    
    * This section contains the sensitive data, encoded in base64. Each key-value pair represents a piece of sensitive information.
        
    * `database-url: dXNlcjpwYXNzd29yZA==`: The base64-encoded value of the database URL. (In this example, it’s `user:password`).
        
    * `secret-key: QW5hbmQgUmF2YWw=` : The base64-encoded value of a secret key. (In this example, it’s `secretkey`).
        
    
    ### Encoding Data to Base64
    
    To create the base64-encoded values for your Secret data:
    
    1. **Encode a Value:**
        
        * Use the `echo` and `base64` commands to encode a value. For example:
            
            ```bash
            bashCopy codeecho -n 'user:password' | base64
            ```
            
        * This will output the base64-encoded string for `user:password`.
            
    2. **Insert Encoded Values:**
        
        * Replace the placeholders in the `secret.yml` file with the base64-encoded values.
            

You can create the Secret by running the following command:

```bash
kubectl apply -f secret.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726068923837/1161b251-59eb-415f-933d-1039ea41c969.png align="center")

**Update the deployment.yaml file to include the Secret**

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
              name: django-secrets
              key: database-url
        - name: SECRET_KEY
          valueFrom:
            secretKeyRef:
              name: django-secrets
              key: secret-key
```

In this example, the `DATABASE_URL` and `SECRET_KEY` environment variables are set from the values in the `django-secrets` Secret.

**Apply the updated deployment using the below command**

```bash
kubectl apply -f deployment.yaml 
```

```bash
kubectl get pods
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726069457747/d7613912-520d-43d6-abd3-c4fb16fb421b.png align="center")

**Verify that the Secret has been created by checking the status of the Secrets in your Namespace.**

To verify that the Secret has been created, you can use the following command:

```bash
kubectl get secrets
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726069487181/6f5803ba-adec-4e87-a853-6c9257f056cf.png align="center")

You can also use the following command to view the details of a specific Secret:

```bash
kubectl describe secret <secret-name> 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726069545450/0d21d5f5-a480-4a5f-bad1-d27955a7f429.png align="center")

To see the key-value pairs of an environment variable in a ConfigMap inside a cluster or a pod.

here, pod name is secret-demo-pod. We used printenv command to see all the environment variables defined in the pod. In secret.yaml file value of password is encryted.

```bash
kubectl exec -it <pod name> -- bash
printenv
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726069656864/623e2cd1-0ec1-44f2-9b85-dda2842f4589.png align="center")

Thankyou for reading !!!!!!!