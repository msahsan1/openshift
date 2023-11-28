<pre>

<h2> Local Storage Class </h2> 
[mahsan@vmrocky8 ~]$  oc get all -n openshift-local-storage
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                                          READY   STATUS    RESTARTS   AGE
pod/local-storage-operator-844f5b5686-glglx   1/1     Running   0          21m

NAME                                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/local-storage-operator   1/1     1            1           21m

NAME                                                DESIRED   CURRENT   READY   AGE
replicaset.apps/local-storage-operator-844f5b5686   1         1         1       21m
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 .crc]$ cd machines/
[mahsan@vmrocky8 machines]$ ll
total 0
drwxr-xr-x 2 mahsan mahsan 140 Nov 28 08:28 crc
[mahsan@vmrocky8 machines]$ cd crc/
[mahsan@vmrocky8 crc]$ ls
config.json  crc.qcow2  id_ecdsa  id_ecdsa.pub  kubeadmin-password  kubeconfig
[mahsan@vmrocky8 crc]$ ssh -i id_ecdsa core@$(crc ip)
Red Hat Enterprise Linux CoreOS 414.92.202310270216-0
  Part of OpenShift 4.14, RHCOS is a Kubernetes native operating system
  managed by the Machine Config Operator (`clusteroperator/machine-config`).

WARNING: Direct SSH access to machines is not recommended; instead,
make configuration changes via `machineconfig` objects:
  https://docs.openshift.com/container-platform/4.14/architecture/architecture-rhcos.html

---
Last login: Sun Nov 26 17:26:35 2023 from 192.168.130.1
[systemd]
Failed Units: 1
  qemu-guest-agent.service
[core@crc-n5gv4-master-0 ~]$

[core@crc-n5gv4-master-0 ~]$ sudo -i
[systemd]
Failed Units: 1
  qemu-guest-agent.service
[root@crc-n5gv4-master-0 ~]# dd if=/dev/zero of=loopbackfile bs=1M count=1000
1000+0 records in
1000+0 records out
1048576000 bytes (1.0 GB, 1000 MiB) copied, 1.73885 s, 603 MB/s
[root@crc-n5gv4-master-0 ~]#  losetup -fP loopbackfile
[root@crc-n5gv4-master-0 ~]# ls -l /dev/loop*
crw-rw----. 1 root disk 10, 237 Nov 28 17:33 /dev/loop-control
brw-rw----. 1 root disk  7,   0 Nov 28 17:33 /dev/loop0
[root@crc-n5gv4-master-0 ~]#

[mahsan@vmrocky8 Local-Storage]$ oc get sc
NAME                                     PROVISIONER                        RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
crc-csi-hostpath-provisioner (default)   kubevirt.io.hostpath-provisioner   Delete          WaitForFirstConsumer   false                  29d
[mahsan@vmrocky8 Local-Storage]$


[mahsan@vmrocky8 Local-Storage]$ oc create -f pvc-localstorage.yml
persistentvolumeclaim/pv-newclaim created

[mahsan@vmrocky8 Local-Storage]$ oc get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                                                 STORAGECLASS                   REASON   AGE
nfs-pv                                     2Gi        RWX            Retain           Available                                                                                                 36h
pv-volume                                  2Gi        RWO            Retain           Available                                                                                                 39h
pv146                                      2Gi        RWO            Recycle          Available                                                                                                 40h
pvc-61bf8f9d-9a87-4ac3-86ad-6cfcfe0bee19   30Gi       RWO            Delete           Bound       myproject/pv-claim                                    crc-csi-hostpath-provisioner            39h
pvc-93dcfc5c-2566-4206-b4a1-5bec7cd85351   30Gi       RWX            Delete           Bound       openshift-image-registry/crc-image-registry-storage   crc-csi-hostpath-provisioner            29d
pvc-adfc5a81-3763-4b6e-86a1-d589f4cc26b8   30Gi       RWO            Delete           Bound       myproject/146pvc                                      crc-csi-hostpath-provisioner            40h
pvc-b29068af-fa3a-4e98-b33d-88b621020f0e   30Gi       RWX            Delete           Bound       myproject/nfs-pv-claim                                crc-csi-hostpath-provisioner            35h
[mahsan@vmrocky8 Local-Storage]$ oc get pvc
NAME          STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS                   AGE
pv-newclaim   Pending                                      crc-csi-hostpath-provisioner   27s
[mahsan@vmrocky8 Local-Storage]$ oc get pvc


</pre>

