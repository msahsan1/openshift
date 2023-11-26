<pre>
<h2> persistant volume </h2>

[mahsan@vmrocky8 ch04]$ oc create -f persistant-vol-claim.yaml
Error from server (Forbidden): error when creating "persistant-vol-claim.yaml": persistentvolumes is forbidden: User "developer" cannot create resource "persistentvolumes" in API group "" at the cluster scope
[mahsan@vmrocky8 ch04]$

[mahsan@vmrocky8 ch04]$ cat persistant-vol-claim.yaml
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume
  labels:
      type: local
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mydata"
	
	
	[mahsan@vmrocky8 ~]$ oc whoami
kubeadmin
[mahsan@vmrocky8 ~]$ oc get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                                                 STORAGECLASS                   REASON   AGE
pvc-93dcfc5c-2566-4206-b4a1-5bec7cd85351   30Gi       RWX            Delete           Bound    openshift-image-registry/crc-image-registry-storage   crc-csi-hostpath-provisioner            27d
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ch04]$ oc whoami
kubeadmin
[mahsan@vmrocky8 ch04]$ oc get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                                                 STORAGECLASS                   REASON   AGE
pv-volume                                  2Gi        RWO            Retain           Available                                                                                                 41s
pvc-93dcfc5c-2566-4206-b4a1-5bec7cd85351   30Gi       RWX            Delete           Bound       openshift-image-registry/crc-image-registry-storage   crc-csi-hostpath-provisioner            27d
[mahsan@vmrocky8 ch04]$

[mahsan@vmrocky8 ch04]$ oc login -u developer -p developer
Login successful.

You have access to the following projects and can switch between them with 'oc project <projectname>':

    hello-openshift
    msa-nginx
  * myproject

Using project "myproject".
[mahsan@vmrocky8 ch04]$ oc whoami
developer
[mahsan@vmrocky8 ch04]$ oc get pv
Error from server (Forbidden): persistentvolumes is forbidden: User "developer" cannot list resource "persistentvolumes" in API group "" at the cluster scope
[mahsan@vmrocky8 ch04]$ oc get pvc
No resources found in myproject namespace.
[mahsan@vmrocky8 ch04]$

<b> Note: Developer do not have permission to access PV only can acces claims </b>

[mahsan@vmrocky8 ch04]$ oc whoami
developer
[mahsan@vmrocky8 ch04]$ oc create -f persistant-vol-claim.yaml
persistentvolumeclaim/pv-claim created
[mahsan@vmrocky8 ch04]$ oc get pv
Error from server (Forbidden): persistentvolumes is forbidden: User "developer" cannot list resource "persistentvolumes" in API group "" at the cluster scope
[mahsan@vmrocky8 ch04]$ oc get pvc
NAME       STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS                   AGE
pv-claim   Pending                                      crc-csi-hostpath-provisioner   13s


<b>  set empty file in CRS vm </b>
[mahsan@vmrocky8 ch04]$ oc whoami
kubeadmin
[mahsan@vmrocky8 ch04]$ cd
[mahsan@vmrocky8 ~]$ cd .crc/machines/
[mahsan@vmrocky8 machines]$ ll
total 0
drwxr-xr-x 2 mahsan mahsan 140 Nov 26 07:38 crc
[mahsan@vmrocky8 machines]$ cd crc/
[mahsan@vmrocky8 crc]$ ls
config.json  crc.qcow2  id_ecdsa  id_ecdsa.pub  kubeadmin-password  kubeconfig
[mahsan@vmrocky8 crc]$ ssh - id_ecdsa core@$(crc ip)
ssh: Could not resolve hostname -: Name or service not known
[mahsan@vmrocky8 crc]$ ssh -i id_ecdsa core@$(crc ip)
Red Hat Enterprise Linux CoreOS 414.92.202310270216-0
  Part of OpenShift 4.14, RHCOS is a Kubernetes native operating system
  managed by the Machine Config Operator (`clusteroperator/machine-config`).

WARNING: Direct SSH access to machines is not recommended; instead,
make configuration changes via `machineconfig` objects:
  https://docs.openshift.com/container-platform/4.14/architecture/architecture-rhcos.html

---
Last login: Sat Nov 25 05:27:29 2023 from 192.168.130.1
[systemd]
Failed Units: 1
  qemu-guest-agent.service
[root@crc-n5gv4-master-0 mnt]#  dd if=/dev/zero of=loopbackfile bs=1M count=1000
1000+0 records in
1000+0 records out
1048576000 bytes (1.0 GB, 1000 MiB) copied, 1.87153 s, 560 MB/s
[root@crc-n5gv4-master-0 mnt]# losetup -fP loopbackfile
[root@crc-n5gv4-master-0 mnt]# ls -ltr /dev/loop*
crw-rw----. 1 root disk 10, 237 Nov 26 17:29 /dev/loop-control
brw-rw----. 1 root disk  7,   0 Nov 26 17:29 /dev/loop0



</pre>
