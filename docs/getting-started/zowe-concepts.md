# Key concepts

Understanding some terminologies and key concepts about Zowe helps you install and work with Zowe effectively.

## Zowe components 

Zowe consists of the following components:
- Zowe Application Framework
- Zowe CLI
- API Mediation Layer
- Zowe Explorer

For detailed information about the different components, see [Zowe components](overview.md).

## Zowe architecture


## Zowe installation

## Instance

An instance is a set of configuration values that enable Zowe to run its server and child processes. An instance is defined in an instance directory, referred to as
INSTANCE_DIR. The INSTANCE_DIR contains an environment file
instance.env, which specifies the configuration values for the instance. These values include the unique set of ports to be used, parameters to control product behaviour,
the unique server name prefix to be used, and the name of the zowe runtime directory where the zowe product files to be run are installed.

The instance is created and configured by the installing user when Zowe is being installed. You can edit the instance files at any time, but these changes will not be applied until you restart the instance.

## Runtime

This is the set of product files to be run. It is stored in a runtime directory, referred to as ROOT_DIR. ROOT_DIR is created when Zowe is installed, either from a convenience build or an SMP/E build. When you upgrade zowe, the installer mechanism replaces all of the old code in ROOT_DIR with the new code. Apart from the installer, ROOT_DIR and its contents are read-only, in order to preserve product integrity.

## Interrelationships between instance and runtime

The purpose of an instance is to separate the user configuration settings from the runtime executable code, so that you can preserve the user settings when the runtime is upgraded, allow users who want different settings to share the same runtime code, or switch an instance to use a different version of the runtime code (if, unusually, you have separate runtimes installed at the same time).

Instance files and runtime files are separate, and you cannot have an INSTANCE_DIR inside a ROOT_DIR or vice-versa.
You can have many instances, and each instance can refer to any single runtime. You should start and stop the execution of a runtime by using the zowe-start.sh and zowe-stop.sh scripts in the INSTANCE_DIR. This starts and stops the instance with the server name prefix specified in instance.env. You must avoid using the same server name prefix in different instances. Once started, an instance provides services to all users who accesses its endpoints.

You can run more than one instance (with different server names) at a time, subject to the capacity of your system.

