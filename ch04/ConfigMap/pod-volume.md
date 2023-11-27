<pre>
<h2> ConfigMap </h2>
 
<b>[mahsan@vmrocky8 ~]$ oc create configmap config --from-literal=foo=lala --from-literal=foo2=lolo </b>
configmap/config created
[mahsan@vmrocky8 ~]$ oc get cm
NAME                       DATA   AGE
config                     2      39s
kube-root-ca.crt           1      44h
openshift-service-ca.crt   1      44h
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ oc get cm -o yaml
apiVersion: v1
items:
- apiVersion: v1
<b>  data:
    foo: lala
    foo2: lolo </b>
  kind: ConfigMap
  metadata:
    creationTimestamp: "2023-11-27T19:02:50Z"
    name: config
    namespace: myproject
    resourceVersion: "424267"
    uid: 420bae5f-7afa-4f02-b10f-eac903b1dbfd
- apiVersion: v1


<b> mahsan@vmrocky8 ~]$ oc describe cm config | more </b>
Name:         config
Namespace:    myproject
Labels:       <none>
Annotations:  <none>

Data
====
foo:
----
lala
foo2:
----
lolo

BinaryData
====

Events:  <none>
<b> ConfigMap file </b>

[mahsan@vmrocky8 ~]$ echo -e "foo3=lili\nfoo4=lele" > config.txt

<b>[mahsan@vmrocky8 ~]$ oc create cm configmap2 --from-file=config.txt </b>
configmap/configmap2 created
[mahsan@vmrocky8 ~]$


[mahsan@vmrocky8 ~]$ oc get cm configmap2 -o yaml
apiVersion: v1
data:
  config.txt: |
    foo3=lili
    foo4=lele
kind: ConfigMap
metadata:
  creationTimestamp: "2023-11-27T19:10:03Z"
  name: configmap2
  namespace: myproject
  resourceVersion: "426019"
  uid: 272af19f-b3cb-4558-bef6-762088a80063
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ echo -e "var1=val1\n# this is a comment\n\nvar2=val2\n#anothercomment" > config.env
[mahsan@vmrocky8 ~]$ cat config.env
var1=val1
# this is a comment

var2=val2
#anothercomment

[mahsan@vmrocky8 ~]$ oc  create cm configmap3 --from-env-file=config.env
configmap/configmap3 created
[mahsan@vmrocky8 ~]$ oc get cm
NAME                       DATA   AGE
config                     2      12m
configmap2                 1      5m40s
configmap3                 2      5s
kube-root-ca.crt           1      45h
openshift-service-ca.crt   1      45h
[mahsan@vmrocky8 ~]$ oc get cm -o yaml

[mahsan@vmrocky8 ~]$ oc get cm configmap3 -o yaml
apiVersion: v1
data:
  var1: val1
  var2: val2
kind: ConfigMap
metadata:
  creationTimestamp: "2023-11-27T19:15:38Z"
  name: configmap3
  namespace: myproject
  resourceVersion: "427388"
  uid: be86843f-e1c9-4e8b-a103-88702ddaace4
[mahsan@vmrocky8 ~]$


[mahsan@vmrocky8 ~]$ oc get cm option  -o yaml
Error from server (NotFound): configmaps "option" not found
[mahsan@vmrocky8 ~]$ oc get cm options -o yaml
apiVersion: v1
data:
  var5: val5
kind: ConfigMap
metadata:

[mahsan@vmrocky8 ~]$ oc run nginx --image=nginx --restart=Never --dry-run -o yaml > pod.yaml
W1127 11:24:48.429483    5042 helpers.go:692] --dry-run is deprecated and can be replaced with --dry-run=client.
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ cat pod.yaml
 
 [mahsan@vmrocky8 ~]$ cat pod.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
    env:
<b>    - name: option # name of the env variable
      valueFrom:
        configMapKeyRef:
          name: options # name of config map
          key: var5 # name of the entity in config map </b>
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

 
[mahsan@vmrocky8 ~]$ vim  pod.yaml
[mahsan@vmrocky8 ~]$ oc create -f pod.yaml
Warning: would violate PodSecurity "restricted:v1.24": allowPrivilegeEscalation != false (container "nginx" must set securityContext.allowPrivilegeEscalation=false), unrestricted capabilities (container "nginx" must set securityContext.capabilities.drop=["ALL"]), runAsNonRoot != true (pod or container "nginx" must set securityContext.runAsNonRoot=true), seccompProfile (pod or container "nginx" must set securityContext.seccompProfile.type to "RuntimeDefault" or "Localhost")
pod/nginx created
[mahsan@vmrocky8 ~]$ oc get pods
NAME                    READY   STATUS    RESTARTS       AGE
146pod                  1/1     Running   1              17h
localvol                2/2     Running   28 (29m ago)   26h
nfs-pv-pod              2/2     Running   4 (28m ago)    13h
nginx                   1/1     Running   0              8s
nginx-c56877d4f-559xl   1/1     Running   2              45h
pv-pod                  1/1     Running   1              17h
test-pod                1/1     Running   1              17h
[mahsan@vmrocky8 ~]$


[mahsan@vmrocky8 ~]$ oc get pods
NAME                    READY   STATUS    RESTARTS       AGE
146pod                  1/1     Running   1              17h
localvol                2/2     Running   28 (29m ago)   26h
nfs-pv-pod              2/2     Running   4 (28m ago)    13h
nginx                   1/1     Running   0              8s
nginx-c56877d4f-559xl   1/1     Running   2              45h
pv-pod                  1/1     Running   1              17h
test-pod                1/1     Running   1              17h
<b> ConfigMap - Volumes </b>

[mahsan@vmrocky8 ~]$ oc create configmap cmvolume --from-literal=var8=mahsan --from-literal=var9=ahsan
configmap/cmvolume created
[mahsan@vmrocky8 ~]$ oc get cm
NAME                       DATA   AGE
cmvolume                   2      71s
config                     2      36m
configmap2                 1      29m
configmap3                 2      23m
kube-root-ca.crt           1      45h
openshift-service-ca.crt   1      45h
options                    1      18m
[mahsan@vmrocky8 ~]$ oc describe cm cmvolume
Name:         cmvolume
Namespace:    myproject
Labels:       <none>
Annotations:  <none>

Data
====
var8:
----
mahsan
var9:
----
ahsan

BinaryData
====

Events:  <none>

[mahsan@vmrocky8 ~]$ oc  run nginx-volume  --image=nginx --restart=Never -o yaml --dry-run > pod-nginx.yaml</b>
W1127 11:44:32.821974    5333 helpers.go:692] --dry-run is deprecated and can be replaced with --dry-run=client.
[mahsan@vmrocky8 ~]$ cat pod-nginx.yaml
<b>apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-volume
  name: nginx-volume
spec:
<b>  volumes: # add a volumes list
  - name: myvolume # just a name, you'll reference this in the pods
    configMap:
      name: cmvolume # name of your configmap </b>
  containers:
  - image: nginx
    name: nginx-volume
    resources: {}
    <b>volumeMounts: # your volume mounts are listed here
    - name: myvolume # the name that you specified in pod.spec.volumes.name
      mountPath: /etc/lala # the path inside your container </b>
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

[mahsan@vmrocky8 ~]$ oc get pods
NAME                    READY   STATUS    RESTARTS       AGE
146pod                  1/1     Running   1              18h
localvol                2/2     Running   28 (52m ago)   27h
nfs-pv-pod              2/2     Running   4 (50m ago)    13h
nginx                   1/1     Running   0              22m
nginx-c56877d4f-559xl   1/1     Running   2              45h
nginx-volume            1/1     Running   0              11s
pv-pod                  1/1     Running   1              17h
test-pod                1/1     Running   1              17h
[mahsan@vmrocky8 ~]$

<b>[mahsan@vmrocky8 ~]$ oc  exec -it nginx-volume -- /bin/sh
# cd /etc/lala
# pwd
/etc/lala
# ls
var8  var9
# cat var8
# ls -ltr
total 0
lrwxrwxrwx. 1 root root 11 Nov 27 19:50 var9 -> ..data/var9
lrwxrwxrwx. 1 root root 11 Nov 27 19:50 var8 -> ..data/var8
# cat var9
ahsan# cat var8

</b>
</pre>
