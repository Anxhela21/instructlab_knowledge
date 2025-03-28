## 2.8. About the virt-operator




The `virt-operator` deploys, upgrades, and manages OpenShift Virtualization without disrupting current virtual machine (VM) workloads.

![virt-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/ac70df070fd6059d06e410b5bbc1801b/cnv_components_virt-operator.png)



<span id="idm139667230446112"></span>
 **Table 2.6. virt-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/virt-api` | HTTP API server that serves as the entry point for all virtualization-related flows. |
|  `deployment/virt-controller` | Observes the creation of a new VM instance object and creates a corresponding pod. When the pod is scheduled on a node, `virt-controller` updates the VM with the node name. |
|  `daemonset/virt-handler` | Monitors any changes to a VM and instructs `virt-launcher` to perform the required operations. This component is node-specific. |
|  `pod/virt-launcher` | Contains the VM that was created by the user as implemented by `libvirt` and `qemu` . |




# Chapter 3. Getting started with OpenShift Virtualization




You can install and configure a basic OpenShift Virtualization environment to explore its features and functionality.

Note
Cluster configuration procedures require `cluster-admin` privileges.



