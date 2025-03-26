## 14.3. Backing up virtual machines




You back up virtual machines (VMs) by creating an OpenShift API for Data Protection (OADP) [Backup custom resource (CR)](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-creating-backup-cr_virt-backing-up-vms) .

The `Backup` CR performs the following actions:

- Backs up OpenShift Virtualization resources by creating an archive file on S3-compatible object storage, such as [Multicloud Object Gateway](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/backup_and_restore/#installing-oadp-mcg) , Noobaa, or Minio.
- Backs up VM disks by using one of the following options:
    
    
    -  [Container Storage Interface (CSI) snapshots](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-backing-up-pvs-csi_virt-backing-up-vms) on CSI-enabled cloud storage, such as Ceph RBD or Ceph FS.
    -  [Restic file system backups](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-backing-up-applications-restic_virt-backing-up-vms) on object storage.
    


Note
OADP provides backup hooks to freeze the VM file system before the backup operation and unfreeze it when the backup is complete.

The `kubevirt-controller` creates the `virt-launcher` pods with annotations that enable Velero to run the `virt-freezer` binary before and after the backup operation.

The `freeze` and `unfreeze` APIs are subresources of the VM snapshot API. See [About virtual machine snapshots](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-about-vm-snapshots_virt-managing-vm-snapshots) for details.



You can add [hooks](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-creating-backup-hooks_virt-backing-up-vms) to the `Backup` CR to run commands on specific VMs before or after the backup operation.

You schedule a backup by creating a [Schedule CR](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#oadp-scheduling-backups_virt-backing-up-vms) instead of a `Backup` CR.

