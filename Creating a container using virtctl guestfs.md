## 8.4. Creating a container using virtctl guestfs




You can use the `virtctl guestfs` command to deploy an interactive container with `libguestfs-tools` and a persistent volume claim (PVC) attached to it.

 **Procedure** 

- To deploy a container with `    libguestfs-tools` , mount the PVC, and attach a shell to it, run the following command:
    
    
    ```
    $ virtctl guestfs -n &lt;namespace&gt; &lt;pvc_name&gt;<span id="CO8-1"><!--Empty--></span><span class="callout">1</span>
    ```
    
    


