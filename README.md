Galleon Feature Pack for integrating datasources into Red Hat JBoss Enterprise Application Platform 
============================================================

This feature pack for JBoss EAP and JBoss EAP XP provides JDBC drivers and datasources for various databases.

The datasources Galleon feature-pack is to be provisioned along with the EAP 7.4, EAP 8 Beta or EAP XP 4 Galleon feature-packs.

The Galleon layers defined in this feature-pack are decorator layers. This means that they need to be provisioned in addition to an EAP base layer.


* EAP 7.4 defined layers [documentation](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_with_jboss_eap_for_openshift_container_platform/capability-trimming-eap-foropenshift_default#available-jboss-eap-layers_default).

* EAP 8 Beta defined layers [documentation](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8-beta/html/using_jboss_eap_on_openshift_container_platform/assembly_capability-trimming-in-jboss-eap-for-openshift_default#available-jboss-eap-layers_assembly_capability-trimming-in-jboss-eap-for-openshift).

* EAP XP 4 defined layers [documentation](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html-single/using_jboss_eap_xp_4.0.0/index#base-provisioning-layers_default).

Resources:

* [Galleon documentation](https://docs.wildfly.org/galleon/)

NOTE: The base layer `datasources-web-server` (that provisions EAP datasources) is the minimal base layer to use when provisioning Galleon layers that this feature-pack define.

## Galleon feature-pack compatible with EAP and EAP XP
>>>>>>> Stashed changes

The Maven coordinates to use is: `org.jboss.eap:eap-datasources-galleon-pack[:<version>]`

NOTE: Version is optional when configuring the EAP 8 Beta channel in the EAP Maven Plugin.

## Supported database types

For each database type it supports, the feature-pack provides 3 Galleon layers that build upon each other :

* One just to add the driver (eg: `postgresql-driver`). This installs a JBoss Modules module for the driver and adds a driver resource to the datasources subsystem in the server configuration.
* One that builds on the first to add a datasource (eg: `postgresql-datasource`).
* One that builds on the second to make the datasource the Jakarta EE default datasource (eg: `postgresql-default-datasource`).

The linked documentation provides information about how to configure each supported database type:

* [Microsoft SQL Server driver and datasource](doc/mssqlserver/README.md)

* [Oracle driver and datasource](doc/oracle/README.md)

* [PostgreSQL driver and datasource](doc/postgresql/README.md)

NOTE: No specific driver version is included in the feature-pack. During provisioning you need to set the environment variable `[driver name]_DRIVER_VERSION`="`<version>`". For example `POSTGRESQL_DRIVER_VERSION="42.2.19"`. Each driver specific environment variable is defined in each driver documentation.

## Using the Datasources Galleon feature-pack

Provisioning of driver and datasources Galleon layers can be done in multiple ways according to the provisioning tooling in use.

### Provisioning using the [EAP 7.4 Galleon support on Openshift](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_with_jboss_eap_for_openshift_online/capability-trimming-eap-foropenshift_default)

You need to set the following environment variables during S2I build to include the drivers and datasources of your choice:

* `GALLEON_PROVISION_FEATURE_PACKS`=`"org.jboss.eap:eap-datasources-galleon-pack:7.4.0.GA-redhat-00003"`
* `GALLEON_PROVISION_LAYERS`="`<base layer>,<datasources layers>`". For example: `"jaxrs-server,postgresql-datasource"`
* `[driver name]_DRIVER_VERSION`="`<driver version>`". For example `POSTGRESQL_DRIVER_VERSION="42.2.19"`

The [todo quickstart](https://github.com/jboss-developer/jboss-eap-quickstarts/tree/EAP_7.4.0.GA/todo-backend) 
contains a complete usage of the EAP datasources Galleon feature-pack and layers.

### Provisioning using the [EAP 8 Beta Maven Plugin](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8-beta/html-single/using_jboss_eap_on_openshift_container_platform/index#assembly_provisioning-a-jboss-eap-server-using-the-maven-plugin_assembly_environment-variables-and-model-expression-resolution) on OpenShift

You need to include the datasources feature-pack and layers in the Maven Plugin configuration. This looks like:

```xml
...
<channels>
  <channel>
    <groupId>org.jboss.eap.channels</groupId>
    <artifactId>eap-8.0-beta</artifactId>
  </channel>
</channels>
<feature-packs>
  <feature-pack>
    <location>org.jboss.eap:wildfly-ee-galleon-pack</location>
  </feature-pack>
  <feature-pack>
    <location>org.jboss.eap.cloud:eap-cloud-galleon-pack</location>
  </feature-pack>
  <feature-pack>
    <location>org.jboss.eap:eap-datasources-galleon-pack</location>
  </feature-pack>
</feature-packs>
<layers>
  <!-- Base layer -->
  <layer>jaxrs-server</layer>
  <layer>postgresql-datasource</layer>
</layers>
...
```

NOTE: The environment variable `[driver name]_DRIVER_VERSION`="`<version>`". For example `POSTGRESQL_DRIVER_VERSION="42.2.19"` must be set when executing an S2I build.

The [todo quickstart](https://github.com/jboss-developer/jboss-eap-quickstarts/tree/8.0.x/todo-backend) contains a complete EAP 8 Beta Maven Plugin configuration.

### Provisioning using the [EAP XP 4 Bootable JAR Maven plugin](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.4/html-single/using_jboss_eap_xp_4.0.0/index#the-bootable-jar_default)

You need to include the datasources feature-pack and layers in the Maven Plugin configuration. This looks like:

```xml
...
<feature-packs>
  <feature-pack>
    <location>org.jboss.eap:wildfly-galleon-pack:4.0.0.GA-redhat-00009</location>
  </feature-pack>
  <feature-pack>
    <location>org.jboss.eap:eap-datasources-galleon-pack:7.4.0.GA-redhat-00003</location>
  </feature-pack>
</feature-packs>
<layers>
  <!-- Base layer -->
  <layer>jaxrs-server</layer>
  <layer>postgresql-datasource</layer>
</layers>
...
```

NOTE: The environment variable `[driver name]_DRIVER_VERSION`="`<version>`". For example `POSTGRESQL_DRIVER_VERSION="42.2.19"` must be set when building an EAP XP Bootable JAR.

The [todo quickstart](https://github.com/jboss-developer/jboss-eap-quickstarts/tree/xp-4.0.x/todo-backend) 
contains a complete EAP XP 4 Bootable JAR Maven Plugin configuration.
