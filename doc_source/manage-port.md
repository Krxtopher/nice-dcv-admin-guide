# Changing the NICE DCV Server TCP port<a name="manage-port"></a>

By default, the NICE DCV server is configured to communicate over port `8443`\. You can specify a custom TCP port after you installed the NICE DCV server\. The port must be higher than 1024\.

You can allow NICE DCV clients to access your NICE DCV server over the standard HTTPS port \(443\)\. To do this, we recommend that you use a web proxy or load balancer as a frontend gateway to redirect client connections to the server\.

Ensure that you communicate any port changes to your clients\. They need the port number to connect to sessions\.

**Topics**
+ [Changing the server TCP port on Windows](#manage-stop-port-windows)
+ [Changing the server TCP port on Linux](#manage-stop-port-linux)

## Changing the NICE DCV Server TCP port on Windows<a name="manage-stop-port-windows"></a>

To change the port that's used by the NICE DCV server, configure the `web-port` parameter using the Windows Registry Editor\.

**To change the TCP port for the server on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **web\-port** parameter\.

   If there's no `web-port` parameter in the registry key, create one:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `web-port` and press **Enter**\.

1. Open the **web\-port** parameter\. For **Value data**, enter the new TCP port number\.
**Note**  
The TCP port number must be higher than 1024\.

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

## Changing the NICE DCV Server TCP port on Linux<a name="manage-stop-port-linux"></a>

To change the port that's used by the NICE DCV server, configure the `web-port` parameter in the `dcv.conf` file\.

**To change the server's TCP port on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `web-port` parameter in the `[connectivity]` section\. Then, replace the existing TCP port number with the new TCP port number\.

   If there's no `web-port` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   web-port=port_number
   ```
**Note**  
The TCP port number must be higher than 1024\.

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.