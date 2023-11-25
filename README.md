<pre>

Started the OpenShift cluster.

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: XXXXX

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
[mahsan@vmrocky8 ~]$ vim login.txt
[mahsan@vmrocky8 ~]$ eval $(crc oc-env)
[mahsan@vmrocky8 ~]$ oc login -u kubeadmin -p XXXXX  https://api.crc.testing:6443
Login successful.

You have access to 66 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ oc get projects
NAME                                               DISPLAY NAME   STATUS
default                                                           Active
hostpath-provisioner                                              Active
kube-node-lease                                                   Active
kube-public                                                       Active
kube-system                                                       Active
openshift                                                         Active
openshift-apiserver                                               Active
openshift-apiserver-operator                                      Active
openshift-authentication                                          Active
openshift-authentication-operator                                 Active
openshift-cloud-controller-manager                                Active
openshift-cloud-controller-manager-operator                       Active
openshift-cloud-credential-operator                               Active
openshift-cloud-network-config-controller                         Active
openshift-cluster-machine-approver                                Active
openshift-cluster-samples-operator                                Active
openshift-cluster-storage-operator                                Active
openshift-cluster-version                                         Active
openshift-config                                                  Active
openshift-config-managed                                          Active
openshift-config-operator                                         Active
openshift-console                                                 Active
openshift-console-operator                                        Active
openshift-console-user-settings                                   Active
openshift-controller-manager                                      Active
openshift-controller-manager-operator                             Active
openshift-dns                                                     Active
openshift-dns-operator                                            Active
openshift-etcd                                                    Active
openshift-etcd-operator                                           Active
openshift-host-network                                            Active
openshift-image-registry                                          Active
openshift-infra                                                   Active
openshift-ingress                                                 Active
openshift-ingress-canary                                          Active
openshift-ingress-operator                                        Active
openshift-kni-infra                                               Active
openshift-kube-apiserver                                          Active
openshift-kube-apiserver-operator                                 Active
openshift-kube-controller-manager                                 Active
openshift-kube-controller-manager-operator                        Active
openshift-kube-scheduler                                          Active
openshift-kube-scheduler-operator                                 Active
openshift-kube-storage-version-migrator                           Active
openshift-kube-storage-version-migrator-operator                  Active
openshift-machine-api                                             Active
openshift-machine-config-operator                                 Active
openshift-marketplace                                             Active
openshift-monitoring                                              Active
openshift-multus                                                  Active
openshift-network-diagnostics                                     Active
openshift-network-node-identity                                   Active
openshift-network-operator                                        Active
openshift-node                                                    Active
openshift-nutanix-infra                                           Active
openshift-oauth-apiserver                                         Active
openshift-openstack-infra                                         Active
openshift-operator-lifecycle-manager                              Active
openshift-operators                                               Active
openshift-ovirt-infra                                             Active
openshift-route-controller-manager                                Active
openshift-sdn                                                     Active
openshift-service-ca                                              Active
openshift-service-ca-operator                                     Active
openshift-user-workload-monitoring                                Active
openshift-vsphere-infra                                           Active
[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ oc login -u developer
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>

[mahsan@vmrocky8 ~]$

[mahsan@vmrocky8 ~]$ cd .crc
[mahsan@vmrocky8 .crc]$ ls -ltr
total 256
-rw------- 1 mahsan mahsan     32 Nov 24 17:42 crc.json
drwxrwxr-x 3 mahsan mahsan     80 Nov 24 17:57 cache
-rw------- 1 mahsan mahsan      8 Nov 24 17:57 segmentIdentifyHash
drwxr-xr-x 3 mahsan mahsan     17 Nov 24 18:01 machines
drwxr-x--- 3 mahsan mahsan     83 Nov 24 20:30 bin
srw-rw-rw- 1 mahsan mahsan      0 Nov 24 20:34 crc-http.sock
-rw------- 1 mahsan mahsan 242901 Nov 24 21:14 crc.log
-rw------- 1 mahsan mahsan   4346 Nov 24 21:14 crcd.log
[mahsan@vmrocky8 .crc]$ cd machines/crc/
[mahsan@vmrocky8 crc]$ ls
config.json  crc.qcow2  id_ecdsa  id_ecdsa.pub  kubeadmin-password  kubeconfig
[mahsan@vmrocky8 crc]$ ssh -i id_ecdsa core@$(crc ip)
The authenticity of host '192.168.130.11 (192.168.130.11)' can't be established.
ECDSA key fingerprint is SHA256:b4amNc4RGU5WODNB9fhxQF4wnUddBRIGcD6GqfoKtHk.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.130.11' (ECDSA) to the list of known hosts.
Red Hat Enterprise Linux CoreOS 414.92.202310270216-0
  Part of OpenShift 4.14, RHCOS is a Kubernetes native operating system
  managed by the Machine Config Operator (`clusteroperator/machine-config`).

WARNING: Direct SSH access to machines is not recommended; instead,
make configuration changes via `machineconfig` objects:
  https://docs.openshift.com/container-platform/4.14/architecture/architecture-rhcos.html

---
[systemd]
Failed Units: 1
  qemu-guest-agent.service
[core@crc-n5gv4-master-0 ~]$ free -m
               total        used        free      shared  buff/cache   available
Mem:           11907        6266         183          91        5900        5641
Swap:              0           0           0




top - 05:28:27 up 43 min,  1 user,  load average: 2.28, 3.47, 3.11
Tasks: 355 total,   1 running, 354 sleeping,   0 stopped,   0 zombie
%Cpu(s):  6.4 us, 11.1 sy,  0.0 ni, 76.7 id,  0.1 wa,  3.6 hi,  1.6 si,  0.6 st
MiB Mem :  11907.7 total,    237.2 free,   6358.6 used,   5755.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   5549.1 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2386 root      20   0 2516912 183656  51292 S  14.6   1.5   4:29.50 kubelet
   3025 root      20   0 2901304   1.2g  63648 S  10.0  10.2   7:29.91 kube-apiserver
      1 root      20   0  178828  22720  10872 S   5.6   0.2   1:07.17 systemd
   1604 root      20   0 3258164 127964  39140 S   5.6   1.0   1:57.31 crio
   3149 root       1 -19   10.7g 300240 129636 S   5.0   2.5   3:02.13 etcd
  64909 core      20   0   26732  18304  10680 S   3.7   0.2   0:01.48 systemd
   2685 root      20   0 1633908 203528  54412 S   2.0   1.7   0:56.19 kube-controller
  10932 1000630+  20   0 1536716 107816  55888 S   1.3   0.9   0:18.63 console
   3213 root      20   0 1672128 144924  48704 S   1.0   1.2   0:22.90 cluster-policy-
   3323 root       2 -18 1258764  41924  21872 S   1.0   0.3   0:25.30 etcd
  11781 1000270+  20   0 1446712  62360  41132 S   1.0   0.5   0:02.73 cluster-samples
  11929 root      20   0 1604156 158720  57308 S   1.0   1.3   0:55.24 authentication-
    696 root      20   0  129096  76216  74712 S   0.7   0.6   0:06.17 systemd-journal
   1003 openvsw+  10 -10  638916 181368  34788 S   0.7   1.5   0:18.81 ovs-vswitchd
   2912 root      20   0 1512664  68680  32612 S   0.7   0.6   0:11.27 kube-scheduler
   8262 nfsnobo+  20   0 1531320 140764  54464 S   0.7   1.2   0:20.53 cluster-openshi
   8699 1000350+  20   0 1521304 131872  47500 S   0.7   1.1   0:16.90 olm
   9488 root      20   0 1460668 103644  53084 S   0.7   0.8   0:21.33 oauth-apiserver
  10891 1000220+  20   0 1508524  46300  34924 S   0.7   0.4   0:11.07 marketplace-ope
  11339 1000350+  20   0 1452396 102428  46460 S   0.7   0.8   0:09.81 catalog
  13538 root      20   0 1718524 238476  77464 S   0.7   2.0   0:45.71 openshift-apise
  13638 nfsnobo+  20   0 1467312 114392  53192 S   0.7   0.9   0:22.75 cluster-etcd-op
  16850 1000130+  20   0 1608748  81660  45272 S   0.7   0.7   0:07.84 ingress-operato
  66032 core      20   0   16388   

[mahsan@vmrocky8 crc]$ oc whoami --show-console
https://console-openshift-console.apps-crc.testing
[mahsan@vmrocky8 crc]$

[mahsan@vmrocky8 crc]$ oc login -u kubeadmin -p XXXXXXX  https://api.crc.testing:6443
Login successful.

You have access to 66 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".


[mahsan@vmrocky8 crc]$ oc get routes -n openshift-console
NAME        HOST/PORT                                      PATH   SERVICES    PORT    TERMINATION          WILDCARD
console     console-openshift-console.apps-crc.testing            console     https   reencrypt/Redirect   None
downloads   downloads-openshift-console.apps-crc.testing          downloads   http    edge/Redirect        None
[mahsan@vmrocky8 crc]$

<b>Developer Create Project using cli </b>

[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$ eval $(crc oc-env)
[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$  oc login -u developer https://api.crc.testing:6443
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>

[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$


[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$ oc new-project hello-openshift \
> --description="This is an example project" \
> --display-name="Hello OpenShift"
Now using project "hello-openshift" on server "https://api.crc.testing:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.43 -- /agnhost serve-hostname


[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$ oc get projects
NAME              DISPLAY NAME      STATUS
hello-openshift   Hello OpenShift   Active
[mahsan@vmrocky8 crc-linux-2.29.0-amd64]$

<h2> Bash Completion </h2>
<b> [mahsan@vmrocky8 openshift]$ source <(oc completion bash) </b>



</pre>
