## 9.9. Triggering virtual machine failover by resolving a failed node




If a node fails and [machine health checks](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/machine_management/#machine-health-checks-about_deploying-machine-health-checks) are not deployed on your cluster, virtual machines (VMs) with `RunStrategy: Always` configured are not automatically relocated to healthy nodes. To trigger VM failover, you must manually delete the `Node` object.

Note
If you installed your cluster by using [installer-provisioned infrastructure](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/installing/#ipi-install-overview) and you properly configured machine health checks:

- Failed nodes are automatically recycled.
- Virtual machines with [RunStrategy](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/virtualization/#virt-about-runstrategies-vms_virt-create-vms) set to `    Always` or `    RerunOnFailure` are automatically scheduled on healthy nodes.




