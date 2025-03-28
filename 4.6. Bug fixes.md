## 4.6. Bug fixes




- Previously, on a large cluster, the OpenShift Virtualization MAC pool manager would take too much time to boot and OpenShift Virtualization might not become ready. With this update, the pool initialization and startup latency is reduced. As a result, VMs can now be successfully defined. ( [BZ#2035344](https://bugzilla.redhat.com/show_bug.cgi?id=2035344) )
- If a Windows VM crashes or hangs during shutdown, you can now manually issue a force shutdown request to stop the VM. ( [BZ#2040766](https://bugzilla.redhat.com/show_bug.cgi?id=2040766) )
- The YAML examples in the VM wizard have now been updated to contain the latest upstream changes. ( [BZ#2055492](https://bugzilla.redhat.com/show_bug.cgi?id=2055492) )
- The **Add Network Interface** button on the VM **Network Interfaces** tab is no longer disabled for non-privileged users. ( [BZ#2056420](https://bugzilla.redhat.com/show_bug.cgi?id=2056420) )
- A non-privileged user can now successfully add disks to a VM without getting a RBAC rule error. ( [BZ#2056421](https://bugzilla.redhat.com/show_bug.cgi?id=2056421) )
- The web console now successfully displays virtual machine templates that are deployed to a custom namespace. ( [BZ#2054650](https://bugzilla.redhat.com/show_bug.cgi?id=2054650) )
- Previously, updating a Single Node OpenShift (SNO) cluster failed if the `    spec.evictionStrategy` field was set to `    LiveMigrate` for a VMI. For live migration to succeed, the cluster must have more than one compute node. With this update, the `    spec.evictionStrategy` field is removed from the virtual machine template in a SNO environment. As a result, cluster update is now successful. ( [BZ#2073880](https://bugzilla.redhat.com/show_bug.cgi?id=2073880) )


