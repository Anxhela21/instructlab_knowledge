## 7.1. About workload security




By default, virtual machine (VM) workloads do not run with root privileges in OpenShift Virtualization.

For each VM, a `virt-launcher` pod runs an instance of `libvirt` in _session mode_ to manage the VM process. In session mode, the `libvirt` daemon runs as a non-root user account and only permits connections from clients that are running under the same user identifier (UID). Therefore, VMs run as unprivileged pods, adhering to the security principle of least privilege.

There are no supported OpenShift Virtualization features that require root privileges. If a feature requires root, it might not be supported for use with OpenShift Virtualization.

