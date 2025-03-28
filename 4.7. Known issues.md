## 4.7. Known issues




- You cannot run OpenShift Virtualization on a single-stack IPv6 cluster. ( [BZ#2193267](https://bugzilla.redhat.com/show_bug.cgi?id=2193267) )
- In a heterogeneous cluster with different compute nodes, virtual machines that have HyperV Reenlightenment enabled cannot be scheduled on nodes that do not support timestamp-counter scaling (TSC) or have the appropriate TSC frequency. ( [BZ#2151169](https://bugzilla.redhat.com/show_bug.cgi?id=2151169) )
- When you use two pods with different SELinux contexts, VMs with the `    ocs-storagecluster-cephfs` storage class fail to migrate and the VM status changes to `    Paused` . This is because both pods try to access the shared `    ReadWriteMany` CephFS volume at the same time. ( [BZ#2092271](https://bugzilla.redhat.com/show_bug.cgi?id=2092271) )
    
    
    - As a workaround, use the `        ocs-storagecluster-ceph-rbd` storage class to live migrate VMs on a cluster that uses Red Hat Ceph Storage.
    
- Restoring a VM snapshot fails if you update OpenShift Container Platform to version 4.11 without also updating OpenShift Virtualization. This is due to a mismatch between the API versions used for snapshot objects. ( [BZ#2159442](https://bugzilla.redhat.com/show_bug.cgi?id=2159442) )
    
    
    - As a workaround, [update OpenShift Virtualization](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#upgrading-virt) to the same minor version as OpenShift Container Platform. To ensure that the versions are kept in sync, use the recommended **Automatic** approval strategy.
    
- Uninstalling OpenShift Virtualization does not remove the node labels created by OpenShift Virtualization. You must remove the labels manually. ( [CNV-22036](https://issues.redhat.com/browse/CNV-22036) )
- The OVN-Kubernetes cluster network provider crashes from peak RAM and CPU usage if you create a large number of `    NodePort` services. This can happen if you use `    NodePort` services to expose SSH access to a large number of virtual machines (VMs). ( [OCPBUGS-1940](https://issues.redhat.com/browse/OCPBUGS-1940) )
    
    
    - As a workaround, use the OpenShift SDN cluster network provider if you want to expose SSH access to a large number of VMs via `        NodePort` services.
    
- Updating to OpenShift Virtualization 4.11 from version 4.10 is blocked until you install the standalone Kubernetes NMState Operator. This occurs even if your cluster configuration does not use any [nmstate](https://nmstate.io/) resources. ( [BZ#2126537](https://bugzilla.redhat.com/show_bug.cgi?id=2126537) )
    
    
    - As a workaround:
        
        
        1. Verify that there are no node network configuration policies defined on the cluster:
            
            
            ```
            $ oc get nncp
            ```
            
            
        1. Choose the appropriate method to update OpenShift Virtualization:
            
            
            1. If the list of node network configuration policies is not empty, exit this procedure and install the [Kubernetes NMState Operator](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/networking/#k8s-nmstate-about-the-k8s-nmstate-operator) to preserve and support your existing nmstate configuration.
            1. If the list is empty, go to step 3.
            
        1. Annotate the `            HyperConverged` custom resource (CR). The following command overwrites any existing JSON patches:
            
            
            ```
            $ oc annotate --overwrite -n openshift-cnv hco kubevirt-hyperconverged 'networkaddonsconfigs.kubevirt.io/jsonpatch=[{"op": "replace","path": "/spec/nmstate", "value": null}]'
            ```
            
            Note
            The `            HyperConverged` object reports a `            TaintedConfiguration` condition while this patch is applied. This is benign.
            
            
            
            
        1. Update OpenShift Virtualization.
        1. After the update completes, remove the annotation by running the following command:
            
            
            ```
            $ oc annotate -n openshift-cnv hco kubevirt-hyperconverged networkaddonsconfigs.kubevirt.io/jsonpatch-
            ```
            
            
        1. Optional: Add back any previously configured JSON patches that were overwritten.
        
    
- Some persistent volume claim (PVC) annotations created by the Containerized Data Importer (CDI) can cause the virtual machine snapshot restore operation to hang indefinitely. ( [BZ#2070366](https://bugzilla.redhat.com/show_bug.cgi?id=2070366) )
    
    
    - As a workaround, you can remove the annotations manually:
        
        
        1. Obtain the [VirtualMachineSnapshotContent](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virtual-machine-snapshot-controller-and-custom-resource-definitions-crds) custom resource (CR) name from the `            status.virtualMachineSnapshotContentName` value in the `            VirtualMachineSnapshot` CR.
        1. Edit the `            VirtualMachineSnapshotContent` CR and remove all lines that contain `            k8s.io/cloneRequest` .
        1. If you did not specify a value for `            spec.dataVolumeTemplates` in the `            VirtualMachine` object, delete any `            DataVolume` and `            PersistentVolumeClaim` objects in this namespace where both of the following conditions are true:
            
            
            1. The object’s name begins with `                restore-` .
            1. The object is not referenced by virtual machines.
                
                This step is optional if you specified a value for `                spec.dataVolumeTemplates` .
                
                
            
        1. Repeat the [restore operation](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-restoring-vm-from-snapshot-cli_virt-managing-vm-snapshots) with the updated `            VirtualMachineSnapshot` CR.
        
    
- Windows 11 virtual machines do not boot on clusters running in [FIPS mode](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/security_hardening/index#con_federal-information-processing-standard-fips_assembly_installing-the-system-in-fips-mode) . Windows 11 requires a TPM (trusted platform module) device by default. However, the `    swtpm` (software TPM emulator) package is incompatible with FIPS. ( [BZ#2089301](https://bugzilla.redhat.com/show_bug.cgi?id=2089301) )
- In a Single Node OpenShift (SNO) cluster, a `    VMCannotBeEvicted` alert occurs on virtual machines that are created from common templates that have the eviction strategy set to `    LiveMigrate` . ( [BZ#2092412](https://bugzilla.redhat.com/show_bug.cgi?id=2092412) )
- The QEMU guest agent on a Fedora 35 virtual machine is blocked by SELinux and does not report data. Other Fedora versions might be affected. ( [BZ#2028762](https://bugzilla.redhat.com/show_bug.cgi?id=2028762) )
    
    
    - As a workaround, disable SELinux on the virtual machine, run the QEMU guest agent commands, and then re-enable SELinux.
    


- If your OpenShift Container Platform cluster uses OVN-Kubernetes as the default Container Network Interface (CNI) provider, you cannot attach a Linux bridge or bonding device to a host’s default interface because of a change in the host network topology of OVN-Kubernetes. ( [BZ#1885605](https://bugzilla.redhat.com/show_bug.cgi?id=1885605) )
    
    
    - As a workaround, you can use a secondary network interface connected to your host, or switch to the OpenShift SDN default CNI provider.
    
- If you use Red Hat Ceph Storage or Red Hat OpenShift Data Foundation Storage, cloning more than 100 VMs at once might fail. ( [BZ#1989527](https://bugzilla.redhat.com/show_bug.cgi?id=1989527) )
    
    
    - As a workaround, you can perform a host-assisted copy by setting `        spec.cloneStrategy: copy` in the storage profile manifest. For example:
        
        
        ```
        apiVersion: cdi.kubevirt.io/v1beta1        kind: StorageProfile        metadata:          name: &lt;provisioner_class&gt;        #   ...        spec:          claimPropertySets:          - accessModes:            - ReadWriteOnce            volumeMode: Filesystem          cloneStrategy: copy<span id="CO1-1"><!--Empty--></span><span class="callout">1</span>status:          provisioner: &lt;provisioner&gt;          storageClass: &lt;provisioner_class&gt;
        ```
        
        
    
- In some instances, multiple virtual machines can mount the same PVC in read-write mode, which might result in data corruption. ( [BZ#1992753](https://bugzilla.redhat.com/show_bug.cgi?id=1992753) )
    
    
    - As a workaround, avoid using a single PVC in read-write mode with multiple VMs.
    
- The Pod Disruption Budget (PDB) prevents pod disruptions for migratable virtual machine images. If the PDB detects pod disruption, then `    openshift-monitoring` sends a `    PodDisruptionBudgetAtLimit` alert every 60 minutes for virtual machine images that use the `    LiveMigrate` eviction strategy. ( [BZ#2026733](https://bugzilla.redhat.com/show_bug.cgi?id=2026733) )
    
    
    - As a workaround, [silence alerts](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/monitoring/#silencing-alerts_managing-alerts) .
    
- OpenShift Virtualization links a service account token in use by a pod to that specific pod. OpenShift Virtualization implements a service account volume by creating a disk image that contains a token. If you migrate a VM, then the service account volume becomes invalid. ( [BZ#2037611](https://bugzilla.redhat.com/show_bug.cgi?id=2037611) )
    
    
    - As a workaround, use user accounts rather than service accounts because user account tokens are not bound to a specific pod.
    
- If you configure the `    HyperConverged` custom resource (CR) to enable mediated devices before drivers are installed, the new device configuration does not take effect. This issue can be triggered by updates. For example, if `    virt-handler` is updated before `    daemonset` , which installs NVIDIA drivers, then nodes cannot provide virtual machine GPUs. ( [BZ#2046298](https://bugzilla.redhat.com/show_bug.cgi?id=2046298) )
    
    
    - As a workaround:
        
        
        1. Remove `            mediatedDevicesConfiguration` and `            permittedHostDevices` from the `            HyperConverged` CR.
        1. Update both `            mediatedDevicesConfiguration` and `            permittedHostDevices` stanzas with the configuration you want to use.
        
    
- If you clone more than 100 VMs using the `    csi-clone` cloning strategy, then the Ceph CSI might not purge the clones. Manually deleting the clones can also fail. ( [BZ#2055595](https://bugzilla.redhat.com/show_bug.cgi?id=2055595) )
    
    
    - As a workaround, you can restart the `        ceph-mgr` to purge the VM clones.
    


# Chapter 5. Installing




