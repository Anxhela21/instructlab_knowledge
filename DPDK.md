# 12.2.3.3. Running a DPDK Checkup Using the Command Line

Use a predefined checkup to verify that your OpenShift Container Platform cluster node can run a virtual machine (VM) with a Data Plane Development Kit (DPDK) workload with zero packet loss. The DPDK checkup runs traffic between a traffic generator and a VM running a test DPDK application.

## Prerequisites

- You have installed the OpenShift CLI (`oc`).
- The cluster is configured to run DPDK applications.
- The project is configured to run DPDK applications.

## Procedure

To run a DPDK checkup, perform the following steps:

1. Create a `ServiceAccount`, `Role`, and `RoleBinding` manifest for the DPDK checkup. Below is an example manifest file:

    ```yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: dpdk-checkup-sa
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      name: kiagnose-configmap-access
    rules:
      - apiGroups: [""]
        resources: ["configmaps"]
        verbs: ["get", "update"]
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: kiagnose-configmap-access
    subjects:
      - kind: ServiceAccount
        name: dpdk-checkup-sa
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: Role
      name: kiagnose-configmap-access
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      name: kubevirt-dpdk-checker
    rules:
      - apiGroups: ["kubevirt.io"]
        resources: ["virtualmachineinstances"]
        verbs: ["create", "get", "delete"]
      - apiGroups: ["subresources.kubevirt.io"]
        resources: ["virtualmachineinstances/console"]
        verbs: ["get"]
      - apiGroups: [""]
        resources: ["configmaps"]
        verbs: ["create", "delete"]
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: kubevirt-dpdk-checker
    subjects:
      - kind: ServiceAccount
        name: dpdk-checkup-sa
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: Role
      name: kubevirt-dpdk-checker
    ```

2. Apply the `ServiceAccount`, `Role`, and `RoleBinding` manifest:

    ```bash
    $ oc apply -n <target_namespace> -f <dpdk_sa_roles_rolebinding>.yaml
    ```

3. Create a ConfigMap manifest containing the input parameters for the checkup. Below is an example ConfigMap:

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: dpdk-checkup-config
      labels:
        kiagnose/checkup-type: kubevirt-dpdk
    data:
      spec.timeout: 10m
      spec.param.networkAttachmentDefinitionName: <network_name>
      spec.param.trafficGenContainerDiskImage: "quay.io/kiagnose/kubevirt-dpdk-checkup-trafficgen:v0.4.0"
      spec.param.vmUnderTestContainerDiskImage: "quay.io/kiagnose/kubevirt-dpdk-checkupvm:v0.4.0"
    ```

4. Apply the ConfigMap manifest:

    ```bash
    $ oc apply -n <target_namespace> -f <dpdk_config_map>.yaml
    ```

5. Create a Job manifest to run the checkup. Below is an example manifest:

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: dpdk-checkup
      labels:
        kiagnose/checkup-type: kubevirt-dpdk
    spec:
      backoffLimit: 0
      template:
        spec:
          serviceAccountName: dpdk-checkup-sa
          restartPolicy: Never
          containers:
            - name: dpdk-checkup
              image: registry.redhat.io/container-native-virtualization/kubevirt-dpdk-checkup-rhel9:v4.17.0
              imagePullPolicy: Always
              securityContext:
                allowPrivilegeEscalation: false
                capabilities:
                  drop: ["ALL"]
                runAsNonRoot: true
                seccompProfile:
                  type: "RuntimeDefault"
              env:
                - name: CONFIGMAP_NAMESPACE
                  value: <target_namespace>
                - name: CONFIGMAP_NAME
                  value: dpdk-checkup-config
    ```

6. Apply the Job manifest:

    ```bash
    $ oc apply -n <target_namespace> -f <dpdk_job>.yaml
    ```

7. Wait for the job to complete:

    ```bash
    $ oc wait job dpdk-checkup -n <target_namespace> --for condition=complete --timeout 10m
    ```

8. Review the results of the checkup:

    ```bash
    $ oc get configmap dpdk-checkup-config -n <target_namespace> -o yaml
    ```

    Example output (success):

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: dpdk-checkup-config
      labels:
        kiagnose/checkup-type: kubevirt-dpdk
    data:
      spec.timeout: 10m
      spec.param.NetworkAttachmentDefinitionName: "dpdk-network-1"
      spec.param.trafficGenContainerDiskImage: "quay.io/kiagnose/kubevirt-dpdk-checkup-trafficgen:v0.4.0"
      spec.param.vmUnderTestContainerDiskImage: "quay.io/kiagnose/kubevirt-dpdk-checkupvm:v0.4.0"
      status.succeeded: "true"
      status.failureReason: ""
      status.startTimestamp: "2023-07-31T13:14:38Z"
      status.completionTimestamp: "2023-07-31T13:19:41Z"
    ```

9. Delete the job and ConfigMap:

    ```bash
    $ oc delete job -n <target_namespace> dpdk-checkup
    $ oc delete configmap -n <target_namespace> dpdk-checkup-config
    ```

10. *(Optional)* Delete the `ServiceAccount`, `Role`, and `RoleBinding`:

    ```bash
    $ oc delete -f <dpdk_sa_roles_rolebinding>.yaml
    ```

## DPDK Checkup ConfigMap Parameters

The following table lists the mandatory and optional parameters you can set in the input ConfigMap:

| Parameter                                   | Description                                                                                     | Is Mandatory |
|---------------------------------------------|-------------------------------------------------------------------------------------------------|--------------|
| `spec.timeout`                              | Time in minutes before the checkup fails.                                                      | True         |
| `spec.param.networkAttachmentDefinitionName`| Name of the `NetworkAttachmentDefinition` object for SR-IOV NICs.                              | True         |
| `spec.param.trafficGenContainerDiskImage`   | Container disk image for the traffic generator.                                                | True         |
| `spec.param.trafficGenTargetNodeName`       | Node for the traffic generator VM.                                                             | False        |
| `spec.param.trafficGenPacketsPerSecond`     | Packets per second (k for kilo, m for million). Default: 8m.                                   | False        |
| `spec.param.vmUnderTestContainerDiskImage`  | Container disk image for the VM under test.                                                    | True         |
| `spec.param.vmUnderTestTargetNodeName`      | Node for the VM under test.                                                                    | False        |
| `spec.param.testDuration`                   | Duration in minutes for the traffic generator to run. Default: 5 minutes.                      | False        |
| `spec.param.portBandwidthGbps`              | Maximum bandwidth of the SR-IOV NIC. Default: 10Gbps.                                          | False        |
| `spec.param.verbose`                        | Set to `true` to increase the verbosity of the checkup log. Default: `false`.                  | False        |

