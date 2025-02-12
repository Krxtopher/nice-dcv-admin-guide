# Post\-Installation checks<a name="setting-up-installing-linux-checks"></a>

This topic provides some post\-installation checks that you should perform after installing NICE DCV to ensure that your NICE DCV server is properly configured\.

**Topics**
+ [Ensure the NICE DCV Server is reachable](#checks-port)
+ [Ensure that the X server is accessible](#checks-xserver)
+ [Verify that DCV GL is properly installed](#checks-gl)

## Ensure the NICE DCV Server is reachable<a name="checks-port"></a>

By default, the NICE DCV server is configured to communicate over port 8443\. Ensure that the server is reachable over this port\. If you have a firewall that prevents access over port 8443, you must change the port over which the NICE DCV server communicates\. For more information, see [Changing the NICE DCV Server TCP port](manage-port.md)\.

Also, if you're setting up NICE DCV on an EC2 instance, create a security group\. This is to enable access to the port over which the NICE DCV server communicates\. For more information, see [how to configure security groups on EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html)\. 

## Ensure that the X server is accessible<a name="checks-xserver"></a>

You must ensure that NICE DCV console and virtual sessions can access the X server\.

### Console Sessions<a name="checks-xserver-console"></a>

When the NICE DCV server is installed, a `dcv` user is created\. Ensure that this user can access the X server\.

**To verify that the `dcv` user can access the X server**  
Run the following command:

```
$ sudo DISPLAY=:0 XAUTHORITY=$(ps aux | grep "X.*\-auth" | grep -v grep | sed -n 's/.*-auth \([^ ]\+\).*/\1/p') xhost | grep "SI:localuser:dcv$"
```

If the command returns `SI:localuser:dcv`, the dcv user can access the X server\.

If the command does not return `SI:localuser:dcv`, the dcv user doesn't have access to the X server\. Run the following commands to restart the X server:
+ RHEL 7\.x/8\.x, CentOs 7\.x/8\.x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x

  ```
  $ sudo systemctl isolate multi-user.target
  ```

  ```
  $ sudo systemctl isolate graphical.target
  ```

### Virtual sessions<a name="checks-xserver-virtual"></a>

If you installed the DCV GL package, you must ensure that local users can access the X server\. This ensures that OpenGL hardware acceleration works correctly with virtual sessions\.

**To verify that local users can access the X server**  
Run the following command:

```
$ sudo DISPLAY=:0 XAUTHORITY=$(ps aux | grep "X.*\-auth" | grep -v grep | sed -n 's/.*-auth \([^ ]\+\).*/\1/p') xhost | grep "LOCAL:$"
```

If the command returns `LOCAL:`, local users can access the X server\.

If the command doesn't return `LOCAL:`, local users don't have access to the X server\. Run the following commands to restart the X server, and to disable and re\-enable DCV GL:
+ RHEL 7\.x/8\.x, CentOs 7\.x/8x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x

  ```
  $ sudo systemctl isolate multi-user.target
  ```

  ```
  $ sudo dcvgladmin disable
  ```

  ```
  $ sudo dcvgladmin enable
  ```

  ```
  $ sudo systemctl isolate graphical.target
  ```

## Verify that DCV GL is properly installed<a name="checks-gl"></a>

The dcvgldiag utility is automatically installed when you install the DCV GL package\. You can use this utility to check that the Linux server configuration meets the DCV GL requirements\.

**To run the dcvgldiag utility**  
Use the following command:

```
$ sudo dcvgldiag
```

The utility returns a list of warnings and errors, along with the possible solutions\.