## 14.2. Backing up and restoring virtual machines




Important
OADP for OpenShift Virtualization is a Technology Preview feature only. Technology Preview features are not supported with Red Hat production service level agreements (SLAs) and might not be functionally complete. Red Hat does not recommend using them in production. These features provide early access to upcoming product features, enabling customers to test functionality and provide feedback during the development process.

For more information about the support scope of Red Hat Technology Preview features, see [Technology Preview Features Support Scope](https://access.redhat.com/support/offerings/techpreview/) .



You back up and restore virtual machines by using the [OpenShift API for Data Protection (OADP)](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#application-backup-restore-operations-overview) .

 **Prerequisites** 

- Access to the cluster as a user with the `    cluster-admin` role.


 **Procedure** 

1. Install the [OADP Operator](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#about-installing-oadp) according to the instructions for your storage provider.
1. Install the [Data Protection Application](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#oadp-installing-dpa_installing-oadp-ocs) with the `    kubevirt` and `    openshift`  [plugins](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#oadp-plugins_oadp-features-plugins) .
1. Back up virtual machines by creating a [Backup custom resource (CR)](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#backing-up-applications) .
1. Restore the `    Backup` CR by creating a [Restore CR](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#restoring-applications) .


