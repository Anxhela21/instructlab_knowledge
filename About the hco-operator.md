## 2.2. About the hco-operator




The `hco-operator` (HCO) provides a single entry point for deploying and managing OpenShift Virtualization and several helper operators with opinionated defaults. It also creates custom resources (CRs) for those operators.

![hco-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/83fc85adcbd43f710a0d0ce14cc0f338/cnv_components_hco-operator.png)



<span id="idm139667252816240"></span>
 **Table 2.1. hco-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/hco-webhook` | Validates the `HyperConverged` custom resource contents. |
|  `deployment/hyperconverged-cluster-cli-download` | Provides the `virtctl` tool binaries to the cluster so that you can download them directly from the cluster. |
|  `KubeVirt/kubevirt-kubevirt-hyperconverged` | Contains all operators, CRs, and objects needed by OpenShift Virtualization. |
|  `SSP/ssp-kubevirt-hyperconverged` | An SSP CR. This is automatically created by the HCO. |
|  `CDI/cdi-kubevirt-hyperconverged` | A CDI CR. This is automatically created by the HCO. |
|  `NetworkAddonsConfig/cluster` | A CR that instructs and is managed by the `cluster-network-addons-operator` . |




