# Configuring NICE DCV authorization<a name="security-authorization"></a>

Authorization is used to grant or deny NICE DCV clients permissions to specific NICE DCV features\. In NICE DCV, authorization is configured using a *permissions file*\. The permissions file defines the specific NICE DCV features that are available to specific users when they connect to a session\.

NICE DCV supports two types of permissions files:

**Topics**
+ [Default permissions file](#security-authorization-default)
+ [Custom permissions file](#security-authorization-custom)
+ [Working with permissions files](security-authorization-file-create.md)

## Default permissions file<a name="security-authorization-default"></a>

If you don't specify a custom permissions file when creating a session, the default permissions file is used for all sessions\. The default permissions file grants only the session owner full access to all features\.

You can customize the default permissions file to include custom authorizations\. The default permissions file is located in `C:\Program Files\NICE\DCV\Server\conf\default.perm` on Windows NICE DCV servers and `/etc/dcv/default.perm` on Linux NICE DCV servers\.

For information about customizing the default permissions file, see [Working with permissions files](security-authorization-file-create.md)\.

## Custom permissions file<a name="security-authorization-custom"></a>

You can use a custom permissions file to define the features that specific users or groups have access to when they connect to a NICE DCV session\. When you use a custom permissions file, you override the default permissions file\.

To use a custom permissions file, you must first create the permissions file\. Next, specify it when you start the session using the `--permissions-file` option with the `dcv create-session` command\. For more information about starting sessions, see [Starting NICE DCV sessions](managing-sessions-start.md)\.

For information about creating a custom permissions file, see [Working with permissions files](security-authorization-file-create.md)\.