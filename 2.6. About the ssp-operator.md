## 2.6. About the ssp-operator




The `ssp-operator` deploys the common templates, the related default boot sources, and the template validator.

![ssp-operator components](https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.11-Virtualization-en-US/images/cf3b5600d66f7d0300e22813330f069f/cnv_components_ssp-operator.png)



<span id="idm139667251094272"></span>
 **Table 2.5. ssp-operator components** 

|  **Component** |  **Description** |
| --- | --- |
|  `deployment/virt-template-validator` | Checks `vm.kubevirt.io/validations` annotations on virtual machines created from templates, and rejects them if they are invalid. |




