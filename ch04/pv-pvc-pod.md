<pre>
<h2> Persistant Volume / Prersistance Volume Claim / </h2> 
[mahsan@vmrocky8 ch04]$ cat pv01.yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv146
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  hostPath:
   path: /tmp
[mahsan@vmrocky8 ch04]$ cat pvc01.yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: 146pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
[mahsan@vmrocky8 ch04]$ cat pvpod.yml
apiVersion: v1
kind: Pod
metadata:
  name: 146pod
spec:
  containers:
    - name: pv-pod
      image: nginx
      volumeMounts:
      - name: mypd
      <b>  mountPath: "/data" </b>
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: 146pvc
[mahsan@vmrocky8 ch04]$

[mahsan@vmrocky8 ch04]<b>$ oc get pv </b>
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                                                 STORAGECLASS                   REASON   AGE
pv146                                      2Gi        RWO            Recycle          Available                                                                                                 11m
pvc-93dcfc5c-2566-4206-b4a1-5bec7cd85351   30Gi       RWX            Delete           Bound       openshift-image-registry/crc-image-registry-storage   crc-csi-hostpath-provisioner            27d
pvc-adfc5a81-3763-4b6e-86a1-d589f4cc26b8   30Gi       RWO            Delete           Bound       myproject/146pvc                                      crc-csi-hostpath-provisioner            6m22s
[mahsan@vmrocky8 ch04]$ <b> oc get pvc </b>
NAME       STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                   AGE
146pvc     Bound     pvc-adfc5a81-3763-4b6e-86a1-d589f4cc26b8   30Gi       RWO            crc-csi-hostpath-provisioner   8m9s
pv-claim   Pending                                                                        crc-csi-hostpath-provisioner   8h
[mahsan@vmrocky8 ch04]$


[mahsan@vmrocky8 ch04]$ <b> oc exec -it 146pod -c pv-pod -- df </b>
Filesystem     1K-blocks     Used Available Use% Mounted on
overlay         31914988 26043996   5870992  82% /
tmpfs              65536        0     65536   0% /dev
shm                65536        0     65536   0% /dev/shm
tmpfs            2438704    82256   2356448   4% /etc/hostname
<b> /dev/vda4       31914988 26043996   5870992  82% /data </b>
tmpfs           11732716       20  11732696   1% /run/secrets/kubernetes.io/serviceaccount
tmpfs            6096756        0   6096756   0% /proc/acpi
tmpfs            6096756        0   6096756   0% /proc/scsi
tmpfs            6096756        0   6096756   0% /sys/firmware
[mahsan@vmrocky8 ch04]$




</pre>




