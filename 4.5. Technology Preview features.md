## 4.5. Technology Preview features




Some features in this release are currently in Technology Preview. These experimental features are not intended for production use. Note the following scope of support on the Red Hat Customer Portal for these features:

 [Technology Preview Features Support Scope](https://access.redhat.com/support/offerings/techpreview) 

- You can now use Microsoft Windows 11 as a guest operating system. However, OpenShift Virtualization 4.11 does not support USB disks, which are required for a critical function of BitLocker recovery. To protect recovery keys, use other methods described in the [BitLocker recovery guide](https://learn.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-recovery-guide-plan) .
- You can now [deploy OpenShift Virtualization on AWS bare metal nodes](https://access.redhat.com/articles/6409731) .
- OpenShift Virtualization has [critical alerts](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-virtualization-alerts) that inform you when a problem occurs that requires immediate attention. Now, each alert has a corresponding description of the problem, a reason for why the alert is occurring, a troubleshooting process to diagnose the source of the problem, and steps for resolving the alert.
- Administrators can now declaratively [create and expose mediated devices](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-configuring-mediated-devices) such as virtual graphics processing units (vGPUs) by editing the `    HyperConverged` CR. Virtual machine owners can then assign these devices to VMs.


- You can [transfer the static IP configuration of the NIC attached to the bridge](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/networking/#capturing-nic-static-ip_k8s-nmstate-updating-node-network-config) by applying a single `    NodeNetworkConfigurationPolicy` manifest to the cluster.


- You can now install OpenShift Virtualization on IBM Cloud bare-metal servers. Bare-metal servers offered by other cloud providers are not supported.


- You can check your OpenShift Virtualization cluster for compliance issues by installing the [Compliance Operator](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/security_and_compliance/#understanding-compliance) and running a scan with the [ocp4-moderate and ocp4-moderate-node profiles](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/security_and_compliance/#compliance-operator-supported-profiles) .


- OpenShift Virtualization now includes a [diagnostic framework](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-running-cluster-checkups) to run predefined checkups that can be used for cluster maintenance and troubleshooting. You can run a predefined checkup to [check network connectivity and latency](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-measuring-latency-vm-secondary-network_virt-running-cluster-checkups) for virtual machines on a secondary network.


- You can create live migration policies with specific parameters, such as bandwidth usage, maximum number of parallel migrations, and timeout, and apply the policies to groups of virtual machines by using virtual machine and namespace labels.


