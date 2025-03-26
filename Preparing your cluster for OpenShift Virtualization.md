## 5.1. Preparing your cluster for OpenShift Virtualization




Review this section before you install OpenShift Virtualization to ensure that your cluster meets the requirements.

Important
You can use any installation method, including user-provisioned, installer-provisioned, or assisted installer, to deploy OpenShift Container Platform. However, the installation method and the cluster topology might affect OpenShift Virtualization functionality, such as snapshots or live migration.



 **Single-node OpenShift differences** 

You can install OpenShift Virtualization on a single-node cluster. See [About single-node OpenShift](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/installing/#install-sno-about-installing-on-a-single-node_install-sno-preparing) for more information. Single-node OpenShift does not support high availability, which results in the following differences:


-  [Pod disruption budgets](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/nodes/#priority-preemption-other_nodes-pods-priority) are not supported.
-  [Live migration](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-live-migration) is not supported.
- Templates or virtual machines that use data volumes or storage profiles must not have the [evictionStrategy](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-configuring-vmi-eviction-strategy) set.


 **FIPS mode** 

If you install your cluster in [FIPS mode](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/installing/#installing-fips-mode_installing-fips) , no additional setup is required for OpenShift Virtualization.


 **IPv6** 

You cannot run OpenShift Virtualization on a single-stack IPv6 cluster. ( [BZ#2193267](https://bugzilla.redhat.com/show_bug.cgi?id=2193267) )


