## 9.1. Creating virtual machines




Use one of these procedures to create a virtual machine:

- Quick Start guided tour
- Quick create from the **Catalog** 
- Pasting a pre-configured YAML file with the virtual machine wizard
- Using the CLI


Warning
Do not create virtual machines in `openshift-*` namespaces. Instead, create a new namespace or use an existing namespace without the `openshift` prefix.



When you create virtual machines from the web console, select a virtual machine template that is configured with a boot source. Virtual machine templates with a boot source are labeled as **Available boot source** or they display a customized label text. Using templates with an available boot source expedites the process of creating virtual machines.

Templates without a boot source are labeled as **Boot source required** . You can use these templates if you complete the steps for [adding a boot source to the virtual machine](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-adding-a-boot-source-web_virt-creating-vm-template) .

Important
Due to differences in storage behavior, some virtual machine templates are incompatible with single-node OpenShift. To ensure compatibility, do not set the `evictionStrategy` field for any templates or virtual machines that use data volumes or storage profiles.



