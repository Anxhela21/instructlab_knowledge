## 8.2. OpenShift Container Platform client commands




The OpenShift Container Platform `oc` client is a command-line utility for managing OpenShift Container Platform resources, including the `VirtualMachine` ( `vm` ) and `VirtualMachineInstance` ( `vmi` ) object types.    


Note
You can use the `-n &lt;namespace&gt;` flag to specify a different project.




<span id="idm139667242461456"></span>
 **Table 8.1. `oc` commands** 

| Command | Description |
| --- | --- |
|  `oc login -u &lt;user_name&gt;` | Log in to the OpenShift Container Platform cluster as `&lt;user_name&gt;` . |
|  `oc get &lt;object_type&gt;` | Display a list of objects for the specified object type in the current project. |
|  `oc describe &lt;object_type&gt; &lt;resource_name&gt;` | Display details of the specific resource in the current project. |
|  `oc create -f &lt;object_config&gt;` | Create a resource in the current project from a file name or from stdin. |
|  `oc edit &lt;object_type&gt; &lt;resource_name&gt;` | Edit a resource in the current project. |
|  `oc delete &lt;object_type&gt; &lt;resource_name&gt;` | Delete a resource in the current project. |




For more comprehensive information on `oc` client commands, see the [OpenShift Container Platform CLI tools](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html-single/cli_tools/#cli-developer-commands) documentation.

