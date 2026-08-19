Galleon Layers
=========

* `mysql-datasource`: Provision the `MySQLDS` non xa datasource. Depends on `mysql-driver` layer.
* `mysql-driver`: Provision the `mysql` driver. This layer installs the JBoss Modules module `com.mysql.jdbc`.

Build time configuration
===============

Configuration to provide when provisioning the Galleon feature-pack.

Required configuration
--------------------------------

* `MYSQL_DRIVER_VERSION`

  * Description: The version of the `com.mysql:mysql-connector-j` Maven artifact.
  * No default value.
  * Required: True
  * System Property: `org.jboss.eap.datasources.mysql.driver.version`

Runtime Configuration
==============

The following set of environment variables and corresponding Java system properties can be used to configure the datasource.

Required configuration
--------------------------------

* `MYSQL_DATABASE`

  * Description: Defines the database name to be used in the datasource's `connection-url` property.
  * No default value.
  * Required: True if `MYSQL_URL` is not set.
  * System Property: `org.jboss.eap.datasources.mysql.database`

* `MYSQL_PASSWORD`

  * Description: Defines the password for the datasource.
  * No default value.
  * Required: True
  * System Property: `org.jboss.eap.datasources.mysql.password`

* `MYSQL_URL`

  * Description: Defines the connection URL for the datasource.
  * Default Value: `jdbc:mysql://${MYSQL_HOST}:${MYSQL_PORT}/${MYSQL_DATABASE}`
  * Required: True if `MYSQL_PORT/HOST/DATABASE` are not set.
  * System Property: `org.jboss.eap.datasources.mysql.connection-url`

* `MYSQL_USER`

  * Description: Defines the username for the datasource.
  * No default value.
  * Required: True
  * System Property: `org.jboss.eap.datasources.mysql.user-name`

Optional configuration
==============

* `MYSQL_BACKGROUND_VALIDATION`

  * Description: When set to true database connections are validated periodically in a background thread prior to use. Defaults to false, meaning the `validate-on-match` method is enabled by default instead.
  * Default Value: `false`
  * System Property: `org.jboss.eap.datasources.mysql.background-validation`

* `MYSQL_BACKGROUND_VALIDATION_MILLIS`

  * Description: Specifies frequency of the validation, in milliseconds, when the `background-validation` database connection validation mechanism is enabled.
  * Default Value: `10000`
  * System Property: `org.jboss.eap.datasources.mysql.background-validation-millis`

* `MYSQL_CONNECTION_CHECKER`

  * Description: Specifies a connection checker class that is used to validate connections. Valid value: `org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLValidConnectionChecker`
  * Default Value: `org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLValidConnectionChecker`
  * System Property: `org.jboss.eap.datasources.mysql.valid-connection-checker-class-name`

* `MYSQL_DATASOURCE`

  * Description: Datasource name used in the `jndi-name`.
  * Default Value: `MySQLDS`
  * System Property: `org.jboss.eap.datasources.mysql.datasource`

* `MYSQL_ENABLED`

  * Description: Set to false to disable the datasource.
  * Default Value: `true`
  * System Property: `org.jboss.eap.datasources.mysql.enabled`

* `MYSQL_EXCEPTION_SORTER`

  * Description: Specifies the exception sorter class that is used to properly detect and clean up after fatal database connection exceptions. Valid value: `org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLExceptionSorter`
  * Default Value: `org.jboss.jca.adapters.jdbc.extensions.mysql.MySQLExceptionSorter`
  * System Property: `org.jboss.eap.datasources.mysql.exception-sorter-class-name`

* `MYSQL_FLUSH_STRATEGY`

  * Description: Specifies how the datasource should be flushed in case of an error.
  * Default Value: `FailingConnectionOnly`
  * System Property: `org.jboss.eap.datasources.mysql.flush-strategy`

* `MYSQL_HOST` (or `MYSQL_SERVICE_HOST`)

  * Description: Defines the database server's host name or IP address to be used in the datasource's `connection-url` property.
  * Default Value: `localhost`
  * Required: True if `MYSQL_URL` is not set.
  * System Property: `org.jboss.eap.datasources.mysql.host`

* `MYSQL_IDLE_TIMEOUT_MINUTES`

  * Description: Specifies the maximum time, in minutes, a connection may be idle before being closed.
  * Default Value: `30`
  * System Property: `org.jboss.eap.datasources.mysql.idle-timeout-minutes`

* `MYSQL_JNDI`

  * Description: Defines the JNDI name for the datasource.
  * Default Value: `java:jboss/datasources/${MYSQL_DATASOURCE}`
  * System Property: `org.jboss.eap.datasources.mysql.jndi-name`

* `MYSQL_JTA`

  * Description: Defines Java Transaction API (JTA) option for the non-XA datasource.
  * Default Value: `true`
  * System Property: `org.jboss.eap.datasources.mysql.jta`

* `MYSQL_MAX_POOL_SIZE`

  * Description: Defines the maximum pool size option for the datasource.
  * Default Value: `20`
  * System Property: `org.jboss.eap.datasources.mysql.max-pool-size`

* `MYSQL_MIN_POOL_SIZE`

  * Description: Defines the minimum pool size option for the datasource.
  * Default Value: `0`
  * System Property: `org.jboss.eap.datasources.mysql.min-pool-size`

* `MYSQL_PORT` (or `MYSQL_SERVICE_PORT`)

  * Description: Defines the database server's port to be used in the datasource's `connection-url` property.
  * Default Value: `3306`
  * Required: True if `MYSQL_URL` is not set.
  * System Property: `org.jboss.eap.datasources.mysql.port`

* `MYSQL_STALE_CONNECTION_CHECKER`

  * Description: Specifies a connection checker class that is used to check stale connections.
  * Default Value: `org.jboss.jca.adapters.jdbc.extensions.novendor.NullStaleConnectionChecker`
  * System Property: `org.jboss.eap.datasources.mysql.stale-connection-checker-class-name`

* `MYSQL_TX_ISOLATION`

  * Description: Defines the `java.sql.Connection` transaction isolation level for the datasource.
  * Default Value: `TRANSACTION_READ_COMMITTED`
  * System Property: `org.jboss.eap.datasources.mysql.transaction-isolation`

* `MYSQL_VALIDATE_ON_MATCH`

  * Description: Indicates whether or not connection level validation should be done when a connection factory attempts to match a managed connection for a given set. This is typically exclusive to the use of background validation.
  * Default Value: `true`
  * System Property: `org.jboss.eap.datasources.mysql.validate-on-match`
