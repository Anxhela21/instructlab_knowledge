## 4.3. New and changed features




- You can now deploy OpenShift Virtualization on a [three-node cluster](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/installing/#installation-three-node-cluster_installing-bare-metal) with zero compute nodes.


- Virtual machines run as unprivileged workloads in _session mode_ by default. This feature improves cluster security by mitigating escalation-of-privilege attacks.


- Red Hat Enterprise Linux (RHEL) 9 is now supported as a guest operating system.


- The link for installing the Migration Toolkit for Virtualization (MTV) Operator in the OpenShift Container Platform web console has been moved. It is now located in the **Related operators** section of the **Getting started resources** card on the **Virtualization** → **Overview** page.


- You can configure the [verbosity level](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-logs) of the `    virtLauncher` , `    virtHandler` , `    virtController` , `    virtAPI` , and `    virtOperator` pod logs to debug specific components by editing the `    HyperConverged` custom resource (CR).


