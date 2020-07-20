# Debugging Zowe Java servers

Zowe has a number of Java tomcat servers.  It is possible to configure Zowe to start these in debug mode and attach a debugger which allows a developer to set breakpoint, inspect variables, step through code, and understand program flow.  Launching Zowe in debug mode has has uses for an extender of Zowe such as helping to onboard their APIs to the API Mediation Layer.  

## Configuring Zowe Java servers for debug

The Zowe runtime `/components` directory contains each of the services.  The API Mediation Layer is started with the `/components/api-mediation/bin/start.sh` script which brings up the three Tomcat servers for the API Gateway, the API Catalog and the API Discovery service.  

The line that brings up each server will be an invocation of the `java` command, such as 

```sh
_BPX_JOBNAME=${ZOWE_PREFIX}${GATEWAY_CODE} java -Xms32m -Xmx256m -Xquickstart \
```

The line with `${GATEWAY_CODE}` is the API Gateway server which is responsible for routing API requests from clients to registered API servers.  `${DISCOVERY_CODE}` will be on the line that starts the API discovery server which is a Spring Boot Eureka service that manages registration of the API servers.  `{CATALOG_CODE}` is the API Catalog that renders the catalog of servers together with their swagger or openAPI description of their APIs and provides Try It Out functionality.  

To debug any of the Java servers it should be brought up in debug mode, and given a port number.  This is done by adding the following parameters to the `java` command:

```
-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address={port}
```

For example, to debug the API Discovery server, add the -Xdebug line to the `/components/api-mediation/bin/start.sh` script below, choosing a suitable free port for `address=`.

```sh
DISCOVERY_CODE=AD
_BPX_JOBNAME=${ZOWE_PREFIX}${DISCOVERY_CODE} java -Xms32m -Xmx256m -Xquickstart \
	-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=26530
    -Dibm.serversocket.recover=true \
    ...
```
When Zowe is started when the `start.sh` script will stop and wait for a debug client to be attached.  `suspend=y` controls whether to pause and wait for a debug client, and `suspend=n` means that the java process continues and does not wait for the debug client to attach.  Which to use depends on the debug scenario being attempted, do you want to look at code involved in the startup sequence of the java server, or do you want to look at a scenario that occurs when everything has started an an action (such as clicking a button, submitting an API request, occurs).



## Debugging Zowe with VS Code
