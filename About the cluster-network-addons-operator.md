## 2.4. About the cluster-network-addons-operator




The `cluster-network-addons-operator` deploys networking components on a cluster and manages the related resources for extended network functionality.

![cluster-network-addons-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/d4f918d242395cd11e9780b35c9bb8f4/cnv_components_cluster-network-addons-operator.png)



<span id="idm139667248386080"></span>
 **Table 2.3. cluster-network-addons-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/kubemacpool-cert-manager` | Manages TLS certificates of Kubemacpool’s webhooks. |
|  `deployment/kubemacpool-mac-controller-manager` | Provides a MAC address pooling service for virtual machine (VM) network interface cards (NICs). |
|  `daemonset/bridge-marker` | Marks network bridges available on nodes as node resources. |
|  `daemonset/kube-cni-linux-bridge-plugin` | Installs CNI plugins on cluster nodes, enabling the attachment of VMs to Linux bridges through network attachment definitions. |




