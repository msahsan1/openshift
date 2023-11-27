<pre>

<h2> Volume NFS </h2>

<b> Persistant Volume </b>
[mahsan@vmrocky8 Volumes]$ cat nfs-pv.yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    path: /data2
    server: 192.168.0.121
    readOnly: false
<b> Persistant Volume Claim </b>
[mahsan@vmrocky8 Volumes]$ cat nfs-pvc.yml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: nfs-pv-claim
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 100Mi
<b> Persistant volume pod </b>
[mahsan@vmrocky8 Volumes]$ cat nfs-pod.yml
kind: Pod
apiVersion: v1
metadata:
   name: nfs-pv-pod
spec:
  volumes:
    - name: nfs-pv
      persistentVolumeClaim:
        claimName: nfs-pv-claim
  containers:
    - name: nfs-client1
      image: busybox
      command:
        - sleep
        - "3600"
      volumeMounts:
        - mountPath: "/nfsshare"
          name: nfs-pv
    - name: nfs-client2
      image: busybox
      command:
        - sleep
        - "3600"
      volumeMounts:
        - mountPath: "/nfsshare"
          name: nfs-pv
[mahsan@vmrocky8 Volumes]$

[mahsan@vmrocky8 Volumes]$ oc get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                                                 STORAGECLASS                   REASON   AGE
nfs-pv                                     2Gi        RWX            Retain           Available                                                                                                 22m
pv-volume                                  2Gi        RWO            Retain           Available                                                                                                 4h19m
pv146                                      2Gi        RWO            Recycle          Available                                                                                                 4h38m
pvc-61bf8f9d-9a87-4ac3-86ad-6cfcfe0bee19   30Gi       RWO            Delete           Bound       myproject/pv-claim                                    crc-csi-hostpath-provisioner            4h15m
pvc-93dcfc5c-2566-4206-b4a1-5bec7cd85351   30Gi       RWX            Delete           Bound       openshift-image-registry/crc-image-registry-storage   crc-csi-hostpath-provisioner            27d
pvc-adfc5a81-3763-4b6e-86a1-d589f4cc26b8   30Gi       RWO            Delete           Bound       myproject/146pvc                                      crc-csi-hostpath-provisioner            4h33m
pvc-b29068af-fa3a-4e98-b33d-88b621020f0e   30Gi       RWX            Delete           Bound       myproject/nfs-pv-claim                                crc-csi-hostpath-provisioner            8m36s
[mahsan@vmrocky8 Volumes]$ oc get pvc
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                   AGE
146pvc         Bound    pvc-adfc5a81-3763-4b6e-86a1-d589f4cc26b8   30Gi       RWO            crc-csi-hostpath-provisioner   4h35m
nfs-pv-claim   Bound    pvc-b29068af-fa3a-4e98-b33d-88b621020f0e   30Gi       RWX            crc-csi-hostpath-provisioner   20m
pv-claim       Bound    pvc-61bf8f9d-9a87-4ac3-86ad-6cfcfe0bee19   30Gi       RWO            crc-csi-hostpath-provisioner   12h
[mahsan@vmrocky8 Volumes]$

[mahsan@vmrocky8 Volumes]$ oc exec -it nfs-pv-pod -c nfs-client1 -- df -h  /nfsshare
Filesystem                Size      Used Available Use% Mounted on
/dev/vda4                30.4G     25.0G      5.4G  82% /nfsshare
[mahsan@vmrocky8 Volumes]$ oc exec -it nfs-pv-pod -c nfs-client2 -- df -h  /nfsshare
Filesystem                Size      Used Available Use% Mounted on
/dev/vda4                30.4G     25.0G      5.4G  82% /nfsshare
[mahsan@vmrocky8 Volumes]$
 
 
 
 </pre>
 

