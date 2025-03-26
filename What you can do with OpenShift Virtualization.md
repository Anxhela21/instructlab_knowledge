## 1.1. What you can do with OpenShift Virtualization




OpenShift Virtualization is an add-on to OpenShift Container Platform that allows you to run and manage virtual machine workloads alongside container workloads.

OpenShift Virtualization adds new objects into your OpenShift Container Platform cluster by using Kubernetes custom resources to enable virtualization tasks. These tasks include:

- Creating and managing Linux and Windows virtual machines
- Connecting to virtual machines through a variety of consoles and CLI tools
- Importing and cloning existing virtual machines
- Managing network interface controllers and storage disks attached to virtual machines
- Live migrating virtual machines between nodes


An enhanced web console provides a graphical portal to manage these virtualized resources alongside the OpenShift Container Platform cluster containers and infrastructure.

OpenShift Virtualization is designed and tested to work well with Red Hat OpenShift Data Foundation features.

Important
When you deploy OpenShift Virtualization with OpenShift Data Foundation, you must create a dedicated storage class for Windows virtual machine disks. See [Optimizing ODF PersistentVolumes for Windows VMs](https://access.redhat.com/articles/6978371) for details.



You can use OpenShift Virtualization with the [OVN-Kubernetes](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/networking/#about-ovn-kubernetes) , [OpenShift SDN](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/networking/#about-openshift-sdn) , or one of the other certified default Container Network Interface (CNI) network providers listed in [Certified OpenShift CNI Plug-ins](https://access.redhat.com/articles/5436171) .

You can check your OpenShift Virtualization cluster for compliance issues by installing the [Compliance Operator](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/security_and_compliance/#understanding-compliance) and running a scan with the `ocp4-moderate` and `ocp4-moderate-node`  [profiles](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/security_and_compliance/#compliance-operator-supported-profiles) . The Compliance Operator uses OpenSCAP, a [NIST-certified tool](https://www.nist.gov/) , to scan and enforce security policies.

Important
OpenShift Virtualization integration with the Compliance Operator is a Technology Preview feature only. Technology Preview features are not supported with Red Hat production service level agreements (SLAs) and might not be functionally complete. Red Hat does not recommend using them in production. These features provide early access to upcoming product features, enabling customers to test functionality and provide feedback during the development process.

For more information about the support scope of Red Hat Technology Preview features, see [Technology Preview Features Support Scope](https://access.redhat.com/support/offerings/techpreview/) .



