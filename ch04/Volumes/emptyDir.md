<pre>
<h2> Openshift Volume emptyDir </h2>
[mahsan@vmrocky8 openshift]$ oc create -f vol-emptdir.yaml
pod/localvol created
[mahsan@vmrocky8 openshift]$ oc get pods
NAME                    READY   STATUS    RESTARTS   AGE
localvol                2/2     Running   0          6s
nginx-c56877d4f-559xl   1/1     Running   1          18h
[mahsan@vmrocky8 openshift]$ cat vol-emptdir.yaml
apiVersion: v1
kind: Pod
metadata:
  name: localvol
spec:
  containers:
  - name: sleepy
    image: busybox
    command:
      - sleep
      - "3600"
    volumeMounts:
      - mountPath: /data
        name: test
  - name: busy
    image: busybox
    command:
      - sleep
      - "3600"
    volumeMounts:
      - mountPath: /data
        name: test
  volumes:
    - name: test
      emptyDir: {}
[mahsan@vmrocky8 openshift]$

[mahsan@vmrocky8 openshift]$ oc describe pod localvol
Name:             localvol
Namespace:        myproject
Priority:         0
Service Account:  default
Node:             crc-n5gv4-master-0/192.168.126.11
Start Time:       Sun, 26 Nov 2023 08:41:00 -0800
Labels:           <none>
Annotations:      k8s.v1.cni.cncf.io/network-status:
                    [{
                        "name": "openshift-sdn",
                        "interface": "eth0",
                        "ips": [
                            "10.217.0.71"
                        ],
                        "default": true,
                        "dns": {}
                    }]
                  openshift.io/scc: restricted-v2
                  seccomp.security.alpha.kubernetes.io/pod: runtime/default
Status:           Running
SeccompProfile:   RuntimeDefault
IP:               10.217.0.71
IPs:
  IP:  10.217.0.71
Containers:
  sleepy:
    Container ID:  cri-o://e88ebd602c3960ab2beeb3809e1719b72c74918d35ad93ef4207c637a74448c4
    Image:         busybox
    Image ID:      docker.io/library/busybox@sha256:023917ec6a886d0e8e15f28fb543515a5fcd8d938edb091e8147db4efed388ee
    Port:          <none>
    Host Port:     <none>
    Command:
      sleep
      3600
    State:          Running
      Started:      Sun, 26 Nov 2023 08:41:03 -0800
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /data from test (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-f898l (ro)
  busy:
    Container ID:  cri-o://c1d03f807a1a7e5510b16d51d046361682fe57b464113e68aa4bf9f999fc26f0
    Image:         busybox
    Image ID:      docker.io/library/busybox@sha256:023917ec6a886d0e8e15f28fb543515a5fcd8d938edb091e8147db4efed388ee
    Port:          <none>
    Host Port:     <none>
    Command:
      sleep
      3600
    State:          Running
      Started:      Sun, 26 Nov 2023 08:41:04 -0800
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /data from test (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-f898l (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  test:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:
    SizeLimit:  <unset>
  kube-api-access-f898l:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
    ConfigMapName:           openshift-service-ca.crt
    ConfigMapOptional:       <nil>
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason          Age   From               Message
  ----    ------          ----  ----               -------
  Normal  Scheduled       99s   default-scheduler  Successfully assigned myproject/localvol to crc-n5gv4-master-0
  Normal  AddedInterface  97s   multus             Add eth0 [10.217.0.71/23] from openshift-sdn
  Normal  Pulling         97s   kubelet            Pulling image "busybox"
  Normal  Pulled          96s   kubelet            Successfully pulled image "busybox" in 1.015613543s (1.015690324s including waiting)
  Normal  Created         96s   kubelet            Created container sleepy
  Normal  Started         96s   kubelet            Started container sleepy
  Normal  Pulling         96s   kubelet            Pulling image "busybox"
  Normal  Pulled          95s   kubelet            Successfully pulled image "busybox" in 900.092785ms (900.107014ms including waiting)
  Normal  Created         95s   kubelet            Created container busy
  Normal  Started         95s   kubelet            Started container busy
[mahsan@vmrocky8 openshift]$


[mahsan@vmrocky8 ~]$ oc exec -it localvol -c sleepy -- sh

~ $ df -h /data/
Filesystem                Size      Used Available Use% Mounted on
/dev/vda4                30.4G     24.8G      5.7G  81% /data
~ $
drwxrwsrwx    2 root     10007500        21 Nov 26 16:48 .
dr-xr-xr-x    1 root     root            74 Nov 26 16:41 ..
-rw-r--r--    1 10007500 10007500        26 Nov 26 16:48 testing
/data $ pwd
/data


[mahsan@vmrocky8 openshift]$ oc exec -it localvol -c busy -- sh
~ $ cat /data/testing
this is for testing only
~ $ hostname


</pre>

