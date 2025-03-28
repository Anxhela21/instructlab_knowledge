## 2.1. How OpenShift Virtualization architecture works




After you install OpenShift Virtualization, the Operator Lifecycle Manager (OLM) deploys operator pods for each component of OpenShift Virtualization:

- Compute: `    virt-operator` 
- Storage: `    cdi-operator` 
- Network: `    cluster-network-addons-operator` 
- Scaling: `    ssp-operator` 
- Templating: `    tekton-tasks-operator` 


OLM also deploys the `hyperconverged-cluster-operator` pod, which is responsible for the deployment, configuration, and life cycle of other components, and several helper pods: `hco-webhook` , and `hyperconverged-cluster-cli-download` .

After all operator pods are successfully deployed, you should create the `HyperConverged` custom resource (CR). The configurations set in the `HyperConverged` CR serve as the single source of truth and the entrypoint for OpenShift Virtualization, and guide the behavior of the CRs.

The `HyperConverged` CR creates corresponding CRs for the operators of all other components within its reconciliation loop. Each operator then creates resources such as daemon sets, config maps, and additional components for the OpenShift Virtualization control plane. For example, when the `hco-operator` creates the `KubeVirt` CR, the `virt-operator` reconciles it and create additional resources such as `virt-controller` , `virt-handler` , and `virt-api` .

The OLM deploys the `hostpath-provisioner-operator` , but it is not functional until you create a `hostpath provisioner` (HPP) CR.

![CNV Deployments](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/bc9d58287306aef0f69431ceb85bfebe/cnv_components_main.png)


 **Additional resources** 

-  [HyperConverged CR configuration](https://github.com/kubevirt/hyperconverged-cluster-operator/blob/main/docs/cluster-configuration.md) 
-  [Virtctl client commands](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-virtctl-commands_virt-using-the-cli-tools) 


