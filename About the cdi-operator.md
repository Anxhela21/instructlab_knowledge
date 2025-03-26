## 2.3. About the cdi-operator




The `cdi-operator` manages the Containerized Data Importer (CDI), and its related resources, which imports a virtual machine (VM) image into a persistent volume claim (PVC) by using a data volume.

![cdi-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/94e34dec2412f854aba205cce5ac852b/cnv_components_cdi-operator.png)



<span id="idm139667239986048"></span>
 **Table 2.2. cdi-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/cdi-apiserver` | Manages the authorization to upload VM disks into PVCs by issuing secure upload tokens. |
|  `deployment/cdi-uploadproxy` | Directs external disk upload traffic to the appropriate upload server pod so that it can be written to the correct PVC. Requires a valid upload token. |
|  `pod/cdi-importer` | Helper pod that imports a virtual machine image into a PVC when creating a data volume. |




