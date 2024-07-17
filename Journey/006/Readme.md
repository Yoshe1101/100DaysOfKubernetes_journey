# ConfigMaps

Config maps are just valumes that are mounted to add configuration files or variable that the application will need.

It is important to dont put any sensitive information in them.

## Prerequisite

For this test we are gonna be using the deploymenys in the folder cm/ of the k8s-specs repo.

To create aConfigMap:

```
kubectl create cm my-config \
--from-file=cm/prometheus-conf.yml
```
And to se the ConfigMap created:

```
kubectl describe cm my-config
```


we create the following pod to check the ConfiMap:

```
kubectl create -f cm/alpine.yml
```

In the section volumes: of the pod deployment is where the configMap name is written:

```
❯ cat cm/alpine.yml                                                                     ─╯
apiVersion: v1
kind: Pod
metadata:
  name: alpine
spec:
  containers:
  - name: alpine
    image: alpine
    command: ["sleep"]
    args: ["100000"]
    volumeMounts:                #volume path mount
    - name: config-vol
      mountPath: /etc/config
  volumes:                       #config map mount
  - name: config-vol
    configMap:
      name: my-config
```


We can create also a configMap based on a folder like:

```
kubectl create cm my-config \
--from-file=cm

```

And if we create this new ConfigMap and we redeploy the pod we will see the new path in the volume path mounted.

To remove the configmap:

```
kubectl delete cm my-config
```

## Declare ConfigMap .yml

Example of config map deployment:

```
kind: ConfigMap 
apiVersion: v1 
metadata:
  name: example-configmap 
data:
  # Configuration values can be set as key-value properties
  database: mongodb
  database_uri: mongodb://localhost:27017
  
  # Or set as complete file contents (even JSON!)
  keys: | 
    image.public.key=771 
    rsa.public.key=42

```

And the we can create the ConfigMap like any other resource:

```
kubectl apply -f config-map.yaml

```

