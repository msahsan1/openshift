<pre>

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: EWBGs-voVxw-wTEmw-VxCsd

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443

[mahsan@vmrocky8 ~]$ eval $(crc oc-env)

<h2> Helm Charts </h2>

[mahsan@vmrocky8 bin]$ sudo curl -L https://mirror.openshift.com/pub/openshift-v4/clients/helm/latest/helm-linux-amd64 -o /usr/local/bin              /helm
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 47.7M  100 47.7M    0     0  9025k      0  0:00:05  0:00:05 --:--:-- 9886k
[mahsan@vmrocky8 bin]$ chmod +x /usr/local/bin/helm
[mahsan@vmrocky8 bin]$ sudo chmod +x /usr/local/bin/helm
[mahsan@vmrocky8 bin]$ chmod +x /usr/local/bin/helm
[mahsan@vmrocky8 bin]$ helm version
version.BuildInfo{Version:"v3.12.1+11.el8", GitCommit:"8cc4ba6fcc61d4c2ad2084c214dda40124bf5d32", GitTreeState:"clean", GoVersion:"go1.1              9.10"}

<b>[mahsan@vmrocky8 bin]$ oc  version --short </b>
Flag --short has been deprecated, This flag is deprecated and will be removed in future. Use 'oc version' instead.
Client Version: 4.14.1
Kustomize Version: v5.0.1
error: You must be logged in to the server (Unauthorized)
[mahsan@vmrocky8 bin]$  helm version
version.BuildInfo{Version:"v3.12.1+11.el8", GitCommit:"8cc4ba6fcc61d4c2ad2084c214dda40124bf5d32", GitTreeState:"clean", GoVersion:"go1.1              9.10"}
[mahsan@vmrocky8 bin]$ ^Ceate deploy myapp1 --image nginx --dry-run=client -o yaml
[mahsan@vmrocky8 bin]$ oc -u login kubeadmin -p EWBGs-voVxw-wTEmw-VxCsd
flags cannot be placed before plugin name: -u
[mahsan@vmrocky8 bin]$ oc -u  kubeadmin -p EWBGs-voVxw-wTEmw-VxCsd
error: unknown shorthand flag: 'u' in -u
See 'oc --help' for usage.

[mahsan@vmrocky8 bin]$ oc create deploy myapp1 --image nginx --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: myapp1
  name: myapp1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: myapp1
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
[mahsan@vmrocky8 bin]$
[mahsan@vmrocky8 bin]$ oc create deploy myapp1 --image bitnami/nginx --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: myapp1
  name: myapp1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: myapp1
    spec:
      containers:
      - image: bitnami/nginx
        name: nginx
        resources: {}
status: {}
[mahsan@vmrocky8 bin]$ oc create deploy myapp1 --image bitnami/nginx --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: myapp1
  name: myapp1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: myapp1
    spec:
      containers:
      - image: bitnami/nginx
        name: nginx
        resources: {}
status: {}
[mahsan@vmrocky8 ch04]$ oc create deploy myapp1 --image bitnami/nginx --dry-run=client -o yaml > nginx-app/templates/deployment.yaml
[mahsan@vmrocky8 ch04]$ cd nginx-app/templates/
[mahsan@vmrocky8 templates]$ ls -ltr
total 4
-rw-rw-r-- 1 mahsan mahsan 396 Nov 30 10:57 deployment.yaml
[mahsan@vmrocky8 templates]$ cd ..
[mahsan@vmrocky8 nginx-app]$ id
uid=1000(mahsan) gid=1000(mahsan) groups=1000(mahsan),10(wheel),983(libvirt)
[mahsan@vmrocky8 nginx-app]$ pwd
/home/mahsan/openshift/ch04/nginx-app
[mahsan@vmrocky8 nginx-app]$ cd ..
[mahsan@vmrocky8 ch04]$ l s-ltt
bash: l: command not found...
[mahsan@vmrocky8 ch04]$ ls -ltr
total 8
drwxrwxr-x 2 mahsan mahsan  101 Nov 27 12:02 ConfigMap
drwxrwxr-x 3 mahsan mahsan 4096 Nov 28 09:36 Volumes
-rw-rw-r-- 1 mahsan mahsan  397 Nov 30 10:56 bitnami-nginx.yaml
drwxrwxr-x 3 mahsan mahsan   23 Nov 30 10:56 nginx-app
[mahsan@vmrocky8 ch04]$ cd nginx-app/
[mahsan@vmrocky8 nginx-app]$ ll
total 0
drwxrwxr-x 2 mahsan mahsan 29 Nov 30 10:57 templates
[mahsan@vmrocky8 nginx-app]$ cd templates/
[mahsan@vmrocky8 templates]$ ll
total 4
-rw-rw-r-- 1 mahsan mahsan 396 Nov 30 10:57 deployment.yaml
[mahsan@vmrocky8 templates]$ cd ..
[mahsan@vmrocky8 nginx-app]$ ll
total 0
drwxrwxr-x 2 mahsan mahsan 29 Nov 30 10:57 templates
[mahsan@vmrocky8 nginx-app]$ vim Chart.yaml
[mahsan@vmrocky8 nginx-app]$ vim Chart.yaml
[mahsan@vmrocky8 nginx-app]$  helm ls
Error: Kubernetes cluster unreachable: the server has asked for the client to provide credentials
[mahsan@vmrocky8 nginx-app]$  helm ls
Error: Kubernetes cluster unreachable: the server has asked for the client to provide credentials
[mahsan@vmrocky8 nginx-app]$ sudo helm ls
sudo: helm: command not found
[mahsan@vmrocky8 nginx-app]$ ls
Chart.yaml  templates
[mahsan@vmrocky8 nginx-app]$ helm version
version.BuildInfo{Version:"v3.12.1+11.el8", GitCommit:"8cc4ba6fcc61d4c2ad2084c214dda40124bf5d32", GitTreeState:"clean", GoVersion:"go1.19.10"}
[mahsan@vmrocky8 nginx-app]$ helm ls
Error: Kubernetes cluster unreachable: the server has asked for the client to provide credentials
[mahsan@vmrocky8 nginx-app]$ Error: Kubernetes cluster unreachable: the server has asked for the client to provide credentials
bash: Error:: command not found...
[mahsan@vmrocky8 nginx-app]$ helm list
Error: Kubernetes cluster unreachable: the server has asked for the client to provide credentials
[mahsan@vmrocky8 nginx-app]$ exit
logout
root@vmrocky8# helm list
Error: Kubernetes cluster unreachable: Get "http://localhost:8080/version": dial tcp [::1]:8080: connect: connection refused
root@vmrocky8# crc status
crc does not seem to be setup correctly, have you run 'crc setup'?
root@vmrocky8# su - mahsan
[mahsan@vmrocky8 ~]$ crc status
CRC VM:          Running
OpenShift:       Starting (v4.14.1)
RAM Usage:       7.784GB of 12.49GB
Disk Usage:      29.74GB of 32.68GB (Inside the CRC VM)
Cache Usage:     23.44GB
Cache Directory: /home/mahsan/.crc/cache
[mahsan@vmrocky8 ~]$ oc list
bash: oc: command not found...
[mahsan@vmrocky8 ~]$ oc get pod
bash: oc: command not found...
[mahsan@vmrocky8 ~]$ eval $(crc oc-env)
[mahsan@vmrocky8 ~]$ oc login   kubeadmin -p EWBGs-voVxw-wTEmw-VxCsd
error: dial tcp: lookup kubeadmin on 127.0.0.1:53: no such host - verify you have provided the correct host and port and that the server is currently running.
[mahsan@vmrocky8 ~]$ oc login -u kubeadmin -p EWBGs-voVxw-wTEmw-VxCsd
Login successful.

You have access to 73 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "declarative-manifests1".
[mahsan@vmrocky8 ~]$ helm version
version.BuildInfo{Version:"v3.12.1+11.el8", GitCommit:"8cc4ba6fcc61d4c2ad2084c214dda40124bf5d32", GitTreeState:"clean", GoVersion:"go1.19.10"}
[mahsan@vmrocky8 ~]$ helm ls
[mahsan@vmrocky8 ~]$ pwd
/home/mahsan
[mahsan@vmrocky8 ~]$ cd openshift/ch04
[mahsan@vmrocky8 ch04]$ ll
total 8
total 4
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 10:57 templates
[mahsan@vmrocky8 nginx-app]$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME          READY   STATUS   RESTARTS   AGE
pod/nginx01   0/1     Error    0          47h
[mahsan@vmrocky8 nginx-app]$ oc whoami
kubeadmin
[mahsan@vmrocky8 nginx-app]$ ll
total 4
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 10:57 templates
[mahsan@vmrocky8 nginx-app]$ helm install nginx-app nginx-app
Error: INSTALLATION FAILED: non-absolute URLs should be in form of repo_name/path_to_chart, got: nginx-app
[mahsan@vmrocky8 nginx-app]$ cd ..

drwxrwxr-x 3 mahsan mahsan 4096 Nov 28 09:36 Volumes
[mahsan@vmrocky8 ch04]$ helm install nginx-app nginx-app
NAME: nginx-app
LAST DEPLOYED: Thu Nov 30 11:07:41 2023
NAMESPACE: declarative-manifests1
STATUS: deployed
REVISION: 1
TEST SUITE: None
[mahsan@vmrocky8 ch04]$ helm ls
NAME            NAMESPACE               REVISION        UPDATED                                 STATUS          CHART           APP VERSION
nginx-app       declarative-manifests1  1               2023-11-30 11:07:41.03328671 -0800 PST  deployed        myapp1-0.1.0    0.1.0
[mahsan@vmrocky8 ch04]$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                         READY   STATUS    RESTARTS   AGE
pod/myapp1-fcdd97fb6-fdms4   0/1     Pending   0          32s
pod/nginx01                  0/1     Error     0          47h

NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/myapp1   0/1     1            0           32s

NAME                               DESIRED   CURRENT   READY   AGE
replicaset.apps/myapp1-fcdd97fb6   1         1         0       32s
[mahsan@vmrocky8 ch04]$  cd nginx-app/
[mahsan@vmrocky8 nginx-app]$ ls -ltr
total 4
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 10:57 templates
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
[mahsan@vmrocky8 nginx-app]$ vi deployment.yaml
[mahsan@vmrocky8 nginx-app]$ cd templates/
[mahsan@vmrocky8 nginx-app]$ cd ..
[mahsan@vmrocky8 ch04]$ ll
total 8
[mahsan@vmrocky8 nginx-app]$  helm install nginx-app2 .
Error: INSTALLATION FAILED: YAML parse error on myapp1/templates/deployment.yaml: error converting YAML to JSON: yaml: line 21: did not find expected key
[mahsan@vmrocky8 nginx-app]$ cd templates/
[mahsan@vmrocky8 templates]$ vim deployment.yaml
[mahsan@vmrocky8 templates]$ cd ..
[mahsan@vmrocky8 nginx-app]$  helm install nginx-app2 .
Error: INSTALLATION FAILED: YAML parse error on myapp1/templates/deployment.yaml: error converting YAML to JSON: yaml: line 21: did not find expected '-' indicator
[mahsan@vmrocky8 nginx-app]$ cd templates/
[mahsan@vmrocky8 templates]$ vim deployment.yaml
[mahsan@vmrocky8 templates]$ cd ..
[mahsan@vmrocky8 nginx-app]$  helm install nginx-app2 .
NAME: nginx-app2
LAST DEPLOYED: Thu Nov 30 11:21:04 2023
NAMESPACE: declarative-manifests1
STATUS: deployed
REVISION: 1
TEST SUITE: None
[mahsan@vmrocky8 nginx-app]$ helm ls
NAME            NAMESPACE               REVISION        UPDATED                                 STATUS          CHART           APP VERSION
nginx-app       declarative-manifests1  1               2023-11-30 11:07:41.03328671 -0800 PST  deployed        myapp1-0.1.0    0.1.0
nginx-app2      declarative-manifests1  1               2023-11-30 11:21:04.173928858 -0800 PST deployed        myapp1-0.1.0    0.1.0
[mahsan@vmrocky8 nginx-app]$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                             READY   STATUS    RESTARTS   AGE
pod/myapp1-fcdd97fb6-fdms4       0/1     Pending   0          18m
pod/nginx-app-7c4f7d58bd-bd9wx   0/1     Pending   0          4m44s
pod/nginx-app-7c4f7d58bd-mfrnb   0/1     Pending   0          4m44s
pod/nginx01                      0/1     Error     0          47h

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/myapp1      0/1     1            0           18m
deployment.apps/nginx-app   0/2     2            0           4m44s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/myapp1-fcdd97fb6       1         1         0       18m
replicaset.apps/nginx-app-7c4f7d58bd   2         2         0       4m44s
[mahsan@vmrocky8 nginx-app]$ ll
total 8
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 11:20 templates
-rw-rw-r-- 1 mahsan mahsan  73 Nov 30 11:17 values.yaml
[mahsan@vmrocky8 nginx-app]$ vim values.yaml
[mahsan@vmrocky8 nginx-app]$ cat Chart.yaml
version: 0.1.0
type: application
name: myapp1
description: My first helm chart
appVersion: "0.1.0"
apiVersion: v2
[mahsan@vmrocky8 nginx-app]$ vim values.yaml
[mahsan@vmrocky8 nginx-app]$ ll
total 8
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 11:20 templates
-rw-rw-r-- 1 mahsan mahsan  81 Nov 30 11:29 values.yaml
[mahsan@vmrocky8 nginx-app]$ helm ls
NAME            NAMESPACE               REVISION        UPDATED                                 STATUS          CHART           APP VERSION
nginx-app       declarative-manifests1  1               2023-11-30 11:07:41.03328671 -0800 PST  deployed        myapp1-0.1.0    0.1.0
nginx-app2      declarative-manifests1  1               2023-11-30 11:21:04.173928858 -0800 PST deployed        myapp1-0.1.0    0.1.0
[mahsan@vmrocky8 nginx-app]$ vim values.yaml
[mahsan@vmrocky8 nginx-app]$ helm upgrade nginx-app2 .
Release "nginx-app2" has been upgraded. Happy Helming!
NAME: nginx-app2
LAST DEPLOYED: Thu Nov 30 11:34:52 2023
NAMESPACE: declarative-manifests1
STATUS: deployed
REVISION: 3
TEST SUITE: None
[mahsan@vmrocky8 nginx-app]$ oc get pod
NAME                         READY   STATUS    RESTARTS   AGE
myapp1-fcdd97fb6-fdms4       0/1     Pending   0          27m
nginx-app-7c4f7d58bd-bd9wx   0/1     Pending   0          13m
nginx-app-7c4f7d58bd-mfrnb   0/1     Pending   0          13m
nginx01                      0/1     Error     0          2d
[mahsan@vmrocky8 nginx-app]$ vim values.yaml
[mahsan@vmrocky8 nginx-app]$ helm upgrade nginx-app2 .
Release "nginx-app2" has been upgraded. Happy Helming!
NAME: nginx-app2
LAST DEPLOYED: Thu Nov 30 11:35:19 2023
NAMESPACE: declarative-manifests1
STATUS: deployed
REVISION: 4
TEST SUITE: None
[mahsan@vmrocky8 nginx-app]$ oc get pod
NAME                         READY   STATUS    RESTARTS   AGE
myapp1-fcdd97fb6-fdms4       0/1     Pending   0          27m
nginx-app-7c4f7d58bd-2skwv   0/1     Pending   0          5s
nginx-app-7c4f7d58bd-7kjnq   0/1     Pending   0          5s
nginx-app-7c4f7d58bd-bd9wx   0/1     Pending   0          14m
nginx-app-7c4f7d58bd-mfrnb   0/1     Pending   0          14m
nginx-app-7c4f7d58bd-nghz7   0/1     Pending   0          5s
nginx01                      0/1     Error     0          2d
[mahsan@vmrocky8 nginx-app]$ helm ls
NAME            NAMESPACE               REVISION        UPDATED                                 STATUS          CHART           APP VERSION
nginx-app       declarative-manifests1  1               2023-11-30 11:07:41.03328671 -0800 PST  deployed        myapp1-0.1.0    0.1.0
nginx-app2      declarative-manifests1  4               2023-11-30 11:35:19.206223373 -0800 PST deployed        myapp1-0.1.0    0.1.0
[mahsan@vmrocky8 nginx-app]$ helm ls
NAME            NAMESPACE               REVISION        UPDATED                                 STATUS          CHART           APP VERSION
nginx-app       declarative-manifests1  1               2023-11-30 11:07:41.03328671 -0800 PST  deployed        myapp1-0.1.0    0.1.0
nginx-app2      declarative-manifests1  6               2023-11-30 11:36:36.828509532 -0800 PST deployed        myapp1-0.1.0    0.1.0
[mahsan@vmrocky8 nginx-app]$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                             READY   STATUS    RESTARTS   AGE
pod/myapp1-fcdd97fb6-fdms4       0/1     Pending   0          29m
pod/nginx-app-7c4f7d58bd-bd9wx   0/1     Pending   0          15m
pod/nginx-app-7c4f7d58bd-mfrnb   0/1     Pending   0          15m
pod/nginx01                      0/1     Error     0          2d

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/myapp1      0/1     1            0           29m
deployment.apps/nginx-app   0/2     2            0           15m

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/myapp1-fcdd97fb6       1         1         0       29m
replicaset.apps/nginx-app-7c4f7d58bd   2         2         0       15m
[mahsan@vmrocky8 nginx-app]$ helm create msa-helpchart
Creating msa-helpchart
[mahsan@vmrocky8 nginx-app]$ ls l-tr
ls: cannot access 'l-tr': No such file or directory
[mahsan@vmrocky8 nginx-app]$ ls -ltr
total 8
-rw-rw-r-- 1 mahsan mahsan 114 Nov 30 10:59 Chart.yaml
drwxrwxr-x 2 mahsan mahsan  29 Nov 30 11:20 templates
-rw-rw-r-- 1 mahsan mahsan  73 Nov 30 11:35 values.yaml
drwxr-xr-x 4 mahsan mahsan  93 Nov 30 11:37 msa-helpchart
[mahsan@vmrocky8 nginx-app]$ cd msa-helpchart/
[mahsan@vmrocky8 msa-helpchart]$ ll
total 8
drwxr-xr-x 2 mahsan mahsan    6 Nov 30 11:37 charts
-rw-r--r-- 1 mahsan mahsan 1149 Nov 30 11:37 Chart.yaml
drwxr-xr-x 3 mahsan mahsan  162 Nov 30 11:37 templates
-rw-r--r-- 1 mahsan mahsan 1880 Nov 30 11:37 values.yaml
[mahsan@vmrocky8 msa-helpchart]$ cat values.yaml
# Default values for msa-helpchart.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1

image:
  repository: nginx
  pullPolicy: IfNotPresent
  # Overrides the image tag whose default is the chart appVersion.
  tag: ""

imagePullSecrets: []
nameOverride: ""
fullnameOverride: ""

serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # Annotations to add to the service account
  annotations: {}
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name: ""

podAnnotations: {}

podSecurityContext: {}
  # fsGroup: 2000

securityContext: {}
  # capabilities:
  #   drop:
  #   - ALL
  # readOnlyRootFilesystem: true
  # runAsNonRoot: true
  # runAsUser: 1000

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: false
  className: ""
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  hosts:
    - host: chart-example.local
      paths:
        - path: /
          pathType: ImplementationSpecific
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

resources: {}
  # We usually recommend not to specify default resources and to leave this as a conscious
  # choice for the user. This also increases chances charts run on environments with little
  # resources, such as Minikube. If you do want to specify resources, uncomment the following
  # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  # limits:
  #   cpu: 100m
  #   memory: 128Mi
  # requests:
  #   cpu: 100m
  #   memory: 128Mi

autoscaling:
  enabled: false
  minReplicas: 1
  maxReplicas: 100
  targetCPUUtilizationPercentage: 80
  # targetMemoryUtilizationPercentage: 80

nodeSelector: {}

tolerations: []

affinity: {}
[mahsan@vmrocky8 msa-helpchart]$ cat charts/
cat: charts/: Is a directory
[mahsan@vmrocky8 msa-helpchart]$ ll
total 8
drwxr-xr-x 2 mahsan mahsan    6 Nov 30 11:37 charts
-rw-r--r-- 1 mahsan mahsan 1149 Nov 30 11:37 Chart.yaml
drwxr-xr-x 3 mahsan mahsan  162 Nov 30 11:37 templates
-rw-r--r-- 1 mahsan mahsan 1880 Nov 30 11:37 values.yaml
[mahsan@vmrocky8 msa-helpchart]$ cat Chart.yaml
apiVersion: v2
name: msa-helpchart
description: A Helm chart for Kubernetes

# A chart can be either an 'application' or a 'library' chart.
#
# Application charts are a collection of templates that can be packaged into versioned archives
# to be deployed.
#
# Library charts provide useful utilities or functions for the chart developer. They're included as
# a dependency of application charts to inject those utilities and functions into the rendering
# pipeline. Library charts do not define any templates and therefore cannot be deployed.
type: application

# This is the chart version. This version number should be incremented each time you make changes
# to the chart and its templates, including the app version.
# Versions are expected to follow Semantic Versioning (https://semver.org/)
version: 0.1.0

# This is the version number of the application being deployed. This version number should be
# incremented each time you make changes to the application. Versions are not expected to
# follow Semantic Versioning. They should reflect the version the application is using.
# It is recommended to use it with quotes.
appVersion: "1.16.0"
[mahsan@vmrocky8 msa-helpchart]$ tree
.
├── charts
├── Chart.yaml
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml

3 directories, 10 files
[mahsan@vmrocky8 msa-helpchart]$

</pre>
