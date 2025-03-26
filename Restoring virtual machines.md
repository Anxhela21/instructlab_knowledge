## 14.4. Restoring virtual machines




You restore an OpenShift API for Data Protection (OADP) `Backup` custom resource (CR) by creating a [Restore CR](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-creating-restore-cr_virt-restoring-vms) .

You can add [hooks](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-creating-restore-hooks_virt-restoring-vms) to the `Restore` CR to run commands in init containers, before the application container starts, or in the application container itself.

