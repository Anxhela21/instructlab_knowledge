## 2.5. About the hostpath-provisioner-operator




The `hostpath-provisioner-operator` deploys and manages the multi-node hostpath provisioner (HPP) and related resources.

![hpp-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/0fc5071df877b64f8d59dc5d793262ce/cnv_components_hpp-operator.png)



<span id="idm139667242491920"></span>
 **Table 2.4. hostpath-provisioner-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/hpp-pool-hpp-csi-pvc-block-&lt;worker_node_name&gt;` | Provides a worker for each node where the hostpath provisioner (HPP) is designated to run. The pods mount the specified backing storage on the node. |
|  `daemonset/hostpath-provisioner-csi` | Implements the Container Storage Interface (CSI) driver interface of the HPP. |
|  `daemonset/hostpath-provisioner` | Implements the legacy driver interface of the HPP. |




