---
layout: docs
title: Configure Airsonic
permalink: /docs/configure/
---
Airsonic has some system-wide configuration. These configurations are stored in the `airsonic.properties` file. There are some exceptions, such as the `airsonic.home` parameter, which are supplied as a Java System Property.

### airsonic.properties file parameters

These parameters are simple key-value pairs stored in a list. It is recommended that these parameters are changed through the web interface settings page. However, they can also be modified directly. Shutdown your server first, modify, then start it for changes to take effect.

### Java parameters

These parameters are not modifiable through the web interface. See below for steps for setting Java Parameters.

###### airsonic.home

This parameter dictates the folder where Airsonic will store its logs, settings, transcode binaries, index and database if using the default H2 database. As such it is recommended to backup this folder.

> Default: `/var/airsonic` or `C:\\music`

#### Setting java parameters on Tomcat

As described in the [RUNNING.txt](http://tomcat.apache.org/tomcat-8.0-doc/RUNNING.txt) doc provided by tomcat, you can create a file named `setenv.sh` or for windows `setenv.bat` in the Tomcat home `bin` folder to  modify  the java args.

Here is an example of a `setenv.sh` file (`setenv.bat` has slightly different syntax):

```
export JAVA_OPTS="$JAVA_OPTS -Dairsonic.home=/home/andrew/.cache/airsonic-test"
```

#### Setting java parameters for stand-alone package (SpringBoot)

When running the standalone package, add `-Dairsonic.home=YOUR_PATH_HERE` to the `java` command line right before the
`-jar` argument. Here is an example for linux (windows users will want to use their OS specific path syntax i.e.
`C:\\your\path`)

```
java -Dairsonic.home=/home/andrew/airsonichome -jar airsonic.war
```

##### Spring Boot/Stand-alone specific configuration

The following configs only apply when running airsonic as a standalone package (i.e. without Tomcat or Jetty). These are only a subset of the connfigurations for spring-boot, the full list can be found [here](https://docs.spring.io/spring-boot/docs/1.4.5.RELEASE/reference/htmlsingle/#common-application-properties). Not that not all configurations apply to airsonic, but the important section is the **# EMBEDDED SERVER CONFIGURATION** section.

###### server.port

This property only applies for spring boot/standalone config. It changes the port that the standalone package listens on.

> Default: 8080

###### server.address

This property only applies for spring boot/standalone config. It changes the address that the standalone package listens on.

> Default: not set and listens to all addresses
