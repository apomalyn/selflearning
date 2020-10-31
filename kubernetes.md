# Kubernetes

## Cheat sheet

### Commands

- `kubectl get <resource> <resource name> -o yaml > definition.yaml` Get the definition of a resource into a yaml
- `kubectl exec -it <pod name> <? container name> <command>` execute a command in a pod
- `kubectl logs -f <pod name> <container name>` get the logs of the selected container
- `kubectl get <resource> --selector <key label>=<label value>[,<key>=<value>,...]`

### Abbreviation and aliases

- **po**: Pod
- **rs**: ReplicaSet
- **deploy**: Deployment
- **svc**: Service
- **ns**: Namespace
- **pv**: PersistentVolume
- **pvc**: PersistentVolumeClaim
- **sa**: ServiceAccount

## Kind

### Pod

Todo definition

#### Definition file

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: <pod name>
  labels:
    # Labels of the pod
spec:
  securityContext:  # Optional
    runAsUser: <user ID>
  containers: # Containers inside the pod
      - name: <container name>
        image: <docker image load inside the container>
        ports:  # Optional
          - containerPort: <port>
          - ...
        env:  # Optional
          - name: <env name>
            value: <env value>
          - name: <env name>
            valueFrom:
              # See ConfigMap or Secret section
        securityContext:  # Optional, if specified override the one from the spec section
          runAsUser: <user ID>
          capabilities:
            add: [<list of capabilities>]
```

#### Multi-container pods

There is multiple types of multi container pod: sidecar, adapter and ambassador.

- A sidecar can be for example a log agent.
- A  adapter container is there to adapt the data from the principal pod to normalize it.
- A ambassador container can be used to make available the data in localhost while the ambassador connect itself to the right resource in function of the environment, for example.

#### Readiness and liveness

The readiness indicate when the container is ready to accept traffic, by default k8s consider that the container is ready as soon as created. To specify a readiness check, add in the container definition:

```yaml
readinessProbe:
  initialDelaySeconds: <number of seconds before the first check> # optional
  periodSeconds: <number of seconds between checks> # optional
  failureThreshold: <number of attempt before considering the container failed> # optional, by default 3

  # For a http check:
  httpGet:
    path: <url to call>
    port: <port to call>

  # For a TCP check:
  tcpSocket:
    port: <port to call>

  # For executing a command:
  exec:
    command:
      - <cmd>
      - <option 1>
      - ...
```

The liveness indicate is the container is running correctly to avoid, for example, the container to continue to run when stuck in a infinite loop. The liveness check has the same syntax and option as the readiness, just replace `readinessProbe` by `livenessProbe`.

#### Volumes

To mount a volume into a pod:
```yaml
spec:
  containers:
    - volumeMounts:
        - name: <name of the volume>
          mountPath: <where to mount the volume on the container>
  volumes:
    - name: <name of the volume>
      # type and details of the volume, head over [here](https://kubernetes.io/docs/concepts/storage/volumes/)
```

#### Commands
- `kubectl run nginx --image=nginx  --dry-run=client -o yaml` generate a pod definition file using the image nginx. The option --dry-run=client do not create the resource, just validate the commands and definition of the resource.

### Replicaset

A replicaset monitor and keep a certain number of pods on the cluster these are called replicas.

#### Definition file

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: <replicaset name>
  labels:
    # Labels of the ReplicaSet
spec:
  replicas: <number total of replicas>
  template:
    # pod definition
  selector:
    matchLabels:
      # labels who can be used to identify the pods (from the template section)
```

#### Commands
- ```kubectl get replicaset```
- ```kubectl delete replicaset <replicaset name>```
- ```kubctl scale -replicas=6 -f <replicaset definition file | replicaset name>``` use the replicaset name will not update the number of replicas in the file definition

### Deployment

The deployment provides the capability to upgrade the underlying instances seamlessly using rolling update, undo changes and pause/resume changes.

#### Definition file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <deployment name>
  labels:
    # Labels of the deployment
spec:
  strategy:
    type: <RollingUpdate | Recreate>
    # Only if RollingUpdate
    rollingUpdate:
      maxSurge: <percent of pods that can be created at the same time> # By default 25%
      maxUnavailable: <percent of pods that can be unavailable at the same time> # By default 25%
  template:
    # pod definition
  replicas: <number of replicas>
  selector:
    matchLabels:
      # labels who can be used to identify the pods (from the template section)
```

#### Commands

- `kubectl create deployment <deployment name> --image=nginx nginx`
- `kubectl create deployment <deployment name> --image=nginx nginx --dry-run=client -o yaml`
- `kubectl rollout status <deployment name>` get the status of the current rolling deployment
- `kubectl rollout undo deployment/<deployment name>` rollback to the previous version of the deployment
- Use the `--record` flag to write the command execution in the resource

### Service

Services are here to allow components to communicate within and outside the application. There is different types of service: NodePort, ClusterIP and LoadBalancer.

#### Definition file

```yaml
apiVersion: v1
kind: Service
metadata:
  name: <name of the service>
  labels:
    # Labels of the service
spec:
  selector:
    <label key of the pod>: <label value>
  type: <NodePort | ClusterIP | LoadBalancer>
  ports:
    # Depends on the type of service
```

#### NodePort

The NodePort make a component available from a port in the node, the port has to be between 30000 and 32767, and will refer to a port on a specify pod.

The ports section under the spec section should be like this:
```yaml
ports:
  - port: <port on the service>  
    targetPort: <port on the pod to target> # By default the targetPort is the same as the port.
    nodePort: <port to call from outside the node, between 30000 and 32767> # Optional
    protocol:

```

#### ClusterIP

ClusterIP allow us to group the pods under a single interface.

The ports section under the spec section should be like this:
```yaml
ports:
  - port: <port of the interface=>
    targetPort: <port of the pods>
```

#### Commands
- `kubectl expose pod <pod to expose> --port=<port to expose> --name <service name>` create a service

### Namespace

#### Definition file

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

To apply resource quota, you need to apply a resource quota file:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: <name of the quota>
  namespace: <apply for which namespace>
spec:
  hard:
    pods: <number of pods allowed>
    requests.cpu:
    requests.memory:
    limits.cpu: <max cpu available for the namespace>
    limits.memory: <max memory available for the namespace>
```

Then execute the following command: `kubectl create -f `

#### Commands

 - `kubectl create -f namespace.yml`
 - `kubectl create namespace <namespace name>`
 - `kubectl config set-context $(kubectl config current-context) --namespace=<namespace name>`: switch default namespace

### ConfigMaps

Are used to pass configuration variable in pods.

#### Definition file

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: <name of the configmap>
data:
  <A VARIABLE>: <value associated>
  <ANOTHER VARIABLE>: <value associated>
```

To use all the variable inside the ConfigMap as environment variables:

```yaml
# Top of the pod definition, under the container section
envFrom:
  - configMapRef:
      name: <configmap name>
```

To use inject the ConfigMap as files, each item inside the configmap become a file with the key as file name and the value inside the file:

```yaml
# Top of the pod definition, under the container section
volumes:
  - name: <volume name>
    configMap:
      name: <config map name>
```

To use a variable from the ConfigMap as a environment variable:

```yaml
# Top of the pod definition, under the container section
env:
  <VARIABLE NAME>:
    valueFrom:
      configMapKeyRef:
        name: <configmap name>
        key: <key of the variable to inject>
```

### Secrets

#### Definition file

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: <name of the secret>
data:
  <A VARIABLE>: <value associated encrypted in base64>
  <ANOTHER VARIABLE>: <value associated encrypted in base64>
```

To use all the variable inside the Secret as environment variables:

```yaml
# Top of the pod definition, under the container section
envFrom:
  - secretRef:
      name: <secret name>
```

To use inject the Secret as files, each item inside the secret become a file with the key as file name and the value inside the file. Definition:

```yaml
# Top of the pod definition, under the container section
volumes:
  - name: <volume name>
    secret:
      secretName: <secret name>
```

To use a variable from the Secret as a environment variable:

```yaml
# Top of the pod definition, under the container section
env:
  <VARIABLE NAME>:
    valueFrom:
      secretKeyRef:
        name: <secret name>
        key: <key of the variable to inject>
```

### ServiceAccount

#### Definition file

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: <name of the service account>
secrets:
  - name: <secret name of the service account>
```

To use set a service account inside a pod, add the following line under the spec node:
```yaml
serviceAccountName: <name of the service account>
```

#### Commands

- `kubectl create serviceaccount <name>` create a service account blank

### Resource

Is used to manage the resource available for each pod.
By default a pod get:
  - CPU: 0.5
  - Memory: 256 Mi

The CPU resource can be expressed in millicore (m) or core (nothing to specify)
The memory can be expressed in:
  - Gigabyte: G
  - Megabyte: M
  - Kilobyte: K
  - Gigibyte: Gi
  - Mebibyte: Mi
  - Kibibyte: Ki

#### Definition file

It can be add directly in the pod definition file under the container node like that:
```yaml
resources:
  requests: # Resources requested as the creation of the container
    memory: <memory allowed>
    cpu: <number of cpu allowed>
  limits: # Resources max allowed for the container
    memory: <max memory allowed>
    cpu: <number max of cpu allowed>
```

### Jobs

#### Definition file

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: <name of the job>
spec:
  completions: <number of successful repetition are needed to consider the job done>
  parallelism: <number of pod started in the same time>
  template:
    spec:
      containers:
        # Definition of containers needed for the job
      restartPolicy: Never
```

### CronJobs

#### Definition file

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: <name of the job>
spec:
  schedule: <schedule of the cron> # Format is: "* * * * *" -> day hour
  jobTemplate:
    spec:
      completions: <number of successful repetition are needed to consider the job done>
      parallelism: <number of pod started in the same time>
      template:
        spec:
          containers:
            # Definition of containers needed for the job
          restartPolicy: Never
```

## Network Policy

### Definition file

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: <name of the policy>
spec:
  podSelector:
    matchLabels:
      # Labels that represent on which pod apply the policy
  policyTypes:
    - <Ingress | Egress >
  ingress:
    - from:
      - podSelector:
          matchLabels:
            # Labels that represent from which pod we will allow incoming traffic
      ports:
        - protocol: <protocol used>
          port: <port available>
```

### Persistent Volume (PV)

A persistent volume is a cluster wide pool of storage volumes configured by an administrator to be uses by users deploying applications on the cluster.

#### Definition file

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: <name of the persistent volume>
spec:
  accessModes:
    - <ReadOnlyMany | ReadWriteOnce | ReadWriteMany >
  capacity:
    storage: <quantity of storage allowed>
  # than insert the type of volume used
```

### Persistent Volume Claim (PVC)

A persistent volume claim is created by the user to access a persistent volume. Each PVC is liked to one PV.

#### Definition file

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: <name of the persistent volume claim>
spec:
  accessModes:
    - <ReadOnlyMany | ReadWriteOnce | ReadWriteMany >
  resources:
    requests:
      storage: <quantity of storage allowed>
```

### StorageClass

Provisionne the storage on the cloud platform, replace a PV.

For more information head over the [Storage documentation](https://kubernetes.io/docs/concepts/storage/storage-classes)

#### Definition file

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: <name of the storage>
provisioner: kubernetes.io/gce-pd

parameters:
  type: <pd-standard | pd-ssd>
  replication-type: <none | regional-pd>
```

## Nodes

### Taints and Tolerances

We can taint a node to avoid pod to be deployed on specific nodes. There is multiple effect possible on a taint:
The effect should be one of:
- NoSchedule:
- PreferNoSchedule:
- NoExecute: kill all pod without the right tolerance

To taint a node do the following:
```bash
kubectl taint nodes <node name> <key name>=<value>:<NoSchedule | PreferNoSchedule | NoExecute>
```

To remove a taint:
```bash
kubectl taint nodes <node name> <key name>:<NoSchedule | PreferNoSchedule | NoExecute>-
```

If we want some pod to be tolerant to a specific taint, add under the section spec:
```yaml
tolerations:
  - key: "<key name>"
    operator: "Equal"
    value: "<value>"
    effect: "<NoSchedule | PreferNoSchedule | NoExecute>"
```

### Node selectors

With node selectors we can insure a specific pod to run on a specific node.

To add a label to a node, run the following command:
```bash
kubectl label nodes <node-name> <label-key>=<label-value>
```
Then add to the pod definition add this under the spec section:
```yaml
nodeSelector:
  <label name>: <value of the label>
```

If you want to deploy a pod on a specific node you can also use (under the spec section):
```yaml
nodeName: <name of the node>
```

### Node affinity & anti-affinity

A node affinity is like a node selector++. It can start a pod on any node that match a specific expression

To add a specific affinity to a pod, add under the spec section:
```yaml
affinity:
  nodeAffinity:
    <affinity type>:
      nodeSelectorTerms:
        - matchExpressions:
          - key: <label name>
            operator: <operator>
            values:
              - <value of the label>
```

| | DuringScheduling | DuringExecution | Description
| ----------- | ----------- | ----------- | ----------- |
| Type 1 | Required | Ignored | During the pod creation, if there is no node available that match expressions given, the pod will not be scheduled |
| Type 2 | Preferred | Ignored | The scheduler will do is best to create the pod in a node matching the given expressions but if it's not possible the pod will be create on a available node |


There is multiple operator, there is some of them:
- In
- NotIn
- Exists: with this operator, the values section isn't needed. It will check if the node contains the label only.

## Metrics and Monitoring

Kubernetes doesn't come with a complete solution for monitoring solution but there is multiple open source solutions (metrics server, prometheus, elastic stack, ...) and proprietary solution (datadog, dynatrace, ...).

### Metrics-Server

To launch metrics-server on minikube, run:
```bash
minikube addons enable metrics-server
```

Otherwise:
```bash
git clone https://github.com/kubernetes-incubator/metrics-server.git
kubectl create -f deploy/1.8+/
```

To see the performance of a node or pod, run:
```bash
kubectl top <node | pod>
```
## Pod design

### Annotations

Annotation are used to record details about the resources.

```yaml
metadata:
  annotations:
    # Annotion for the resource
```
## Ingress

Ingress networking is divided in two parts: controller and resource.
Kubernetes doesn't come with a built in ingress controller, there is a multiple options availables like: nginx, istio, traefik, HAProxy, etc...

### Controller

The controller will need:
- a Deployment
- a Service
- a ConfigMap
- a ServiceAccount

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <name of the ingress controller>
spec:
  replicas: 1
  selector:
    matchLabels:
      name: <name of the pod>
  template:
    metadata:
      labels:
        name: <name of the pod>
    spec:
      containers:
        - name: <name of the container>
          image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:<latest version>
          args:
            - /nginx-ingress-controller
            - --configmap=${POD_NAMESPACE}/<config map name>
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443          
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: <name of the service>
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
      name: http
    - port: 443
      targetPort: 443
      protocol: TCP
      name: https
  selector:
    name: <name of the pod>
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: <name of the config map>
data:
  # Ingress controller configuration
```

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: <name of the service account>
secrets:
  # Secrets of Roles, ClusterRoles and RoleBindings
```

### Resource

The ingress resource will contains the routing and rules for the incoming traffic.

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: <name of the resource>
spec:
  rules: # Contains all the rules for the resource.
    - host: <host to apply the rule> # Optional, by default "*"
      http: # Template for a http rule
        paths:
          - path: <http path that will react> # Optional, by default "*"
            backend:
              serviceName: <name of the service to make available through ingress>
              servicePort: <port to expose>
```
