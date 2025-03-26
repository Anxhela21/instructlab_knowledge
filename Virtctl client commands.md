## 8.3. Virtctl client commands




The `virtctl` client is a command-line utility for managing OpenShift Virtualization resources.

To view a list of `virtctl` commands, run the following command:

```
$ virtctl help
```

To view a list of options that you can use with a specific command, run it with the `-h` or `--help` flag. For example:

```
$ virtctl image-upload -h
```

To view a list of global command options that you can use with any `virtctl` command, run the following command:

```
$ virtctl options
```

The following table contains the `virtctl` commands used throughout the OpenShift Virtualization documentation.


<span id="idm139667245738176"></span>
 **Table 8.2. `virtctl` client commands** 

| Command | Description |
| --- | --- |
|  `virtctl start &lt;vm_name&gt;` | Start a virtual machine. |
|  `virtctl start --paused &lt;vm_name&gt;` | Start a virtual machine in a paused state. This option enables you to interrupt the boot process from the VNC console. |
|  `virtctl stop &lt;vm_name&gt;` | Stop a virtual machine. |
|  `virtctl stop &lt;vm_name&gt; --grace-period 0 --force` | Force stop a virtual machine. This option might cause data inconsistency or data loss. |
|  `virtctl pause vm|vmi &lt;object_name&gt;` | Pause a virtual machine or virtual machine instance. The machine state is kept in memory. |
|  `virtctl unpause vm|vmi &lt;object_name&gt;` | Unpause a virtual machine or virtual machine instance. |
|  `virtctl migrate &lt;vm_name&gt;` | Migrate a virtual machine. |
|  `virtctl restart &lt;vm_name&gt;` | Restart a virtual machine. |
|  `virtctl expose &lt;vm_name&gt;` | Create a service that forwards a designated port of a virtual machine or virtual machine instance and expose the service on the specified port of the node. |
|  `virtctl console &lt;vmi_name&gt;` | Connect to a serial console of a virtual machine instance. |
|  `virtctl vnc --kubeconfig=$KUBECONFIG &lt;vmi_name&gt;` | Open a VNC (Virtual Network Client) connection to a virtual machine instance. Access the graphical console of a virtual machine instance through a VNC which requires a remote viewer on your local machine. |
|  `virtctl vnc --kubeconfig=$KUBECONFIG --proxy-only=true &lt;vmi-name&gt;` | Display the port number and connect manually to the virtual machine instance by using any viewer through the VNC connection. |
|  `virtctl vnc --kubeconfig=$KUBECONFIG --port=&lt;port-number&gt; &lt;vmi-name&gt;` | Specify a port number to run the proxy on the specified port, if that port is available. If a port number is not specified, the proxy runs on a random port. |
|  `virtctl image-upload dv &lt;datavolume_name&gt; --image-path=&lt;/path/to/image&gt; --no-create` | Upload a virtual machine image to a data volume that already exists. |
|  `virtctl image-upload dv &lt;datavolume_name&gt; --size=&lt;datavolume_size&gt; --image-path=&lt;/path/to/image&gt;` | Upload a virtual machine image to a new data volume. |
|  `virtctl version` | Display the client and server version information. |
|  `virtctl fslist &lt;vmi_name&gt;` | Return a full list of file systems available on the guest machine. |
|  `virtctl guestosinfo &lt;vmi_name&gt;` | Return guest agent information about the operating system. |
|  `virtctl userlist &lt;vmi_name&gt;` | Return a full list of logged-in users on the guest machine. |




