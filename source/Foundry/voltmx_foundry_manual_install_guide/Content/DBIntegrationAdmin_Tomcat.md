<!-- Commented out to hide weblogic content -->

                              

<!-- Create and Configure a Database for **VoltMX Admin**
-----------------------------------------------------

To create a database for **Admin**, follow these steps:

1.  Create a database for admin with a custom name along with prefix and suffix. Prefix and suffix are optional. For example, database name is `<prefix>admindb<suffix>`.
    
    > **_Note:_**  For Oracle databases, a schema name should be in capital letters.  
      Find the word `adminDB` in SQL files located in the admin scripts and replace it with `ADMINDB`.
    
    > **_Note:_** For Oracle, create necessary tablespaces and Users before proceeding. Refer to [Prerequisites for Volt MX Foundry with Oracle](Database_Prerequsites.md#prerequisites-for-volt-mx-foundry-with-oracle).
    
    Volt MX
    
    **The following is a sample query for creating a database in MSSQL:**
    
    `CREATE DATABASE admindb;`
    
    The following is a sample query for creating a database in MySQL:
    
    ```CREATE DATABASE \`<DBNAME>\` DEFAULT CHARACTER SET utf8 COLLATE utf8\_unicode\_ci;

    
2.  The following details are required for Flyway configuration:
    
    *   Schema name for Admin: `admindb`
    *   Placeholders for Admin:


### For Admin (admindb), replace the following placeholders in SQL migrations for your database flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_TYPE -> value must be 

```
    mysql/oracle/sqlserver based on the chosen databases.
    
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_HOSTNAME -> database host name where 
    admindb is created.
    
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_PORT -> database port where 
    admindb is created.
    
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_USERNAME -> database user name
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_PASSWORD ->:  ([Encrypt](Encrypt_Passwords.md) this password)
          - For MySQL and SQL Server: database user password 
    
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_INSTANCE ->  MySQL – empty, 
    SQL Server – instance name if given, Oracle - SID name. flyway.placeholders.VOLTMX_SERVER_CACHEID_TRANSPORT=""flyway.placeholders.VOLTMX_SERVER_SESSION_DISTRIBUTED="FALSE"  
    flyway.placeholders.VOLTMX_SERVER_CACHE_TYPE="EHCACHE"  
    flyway.placeholders.VOLTMX_SERVER_CACHE_URL="" flyway.placeholders.VOLTMX_SERVER_JMS_INITIAL_CONTEXT_FACTORY=""
    flyway.placeholders.VOLTMX_SERVER_JMS_PROVIDER_URL=""
    flyway.placeholders.VOLTMX_SERVER_JMS_USER_NAME=""
    flyway.placeholders.VOLTMX_SERVER_JMS_USER_PASSWORD="" ([Encrypt](Encrypt_Passwords.md) this password) flyway.placeholders.VOLTMX_SERVER_KEYSTORE_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_LOG_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_MEMCACHED_COUNT=""
    flyway.placeholders.VOLTMX_SERVER_MEMCACHE_CLUSTER=""
    flyway.placeholders.VOLTMX_SERVER_RICH_CLIENT_DEPLOY=""
    flyway.placeholders.VOLTMX_SERVER_TRUSTSTORE_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_TRUSTSTORE_PASSWORD=""  ([Encrypt](Encrypt_Passwords.md) this password)
    flyway.placeholders.VOLTMX_SERVER_LOG_OPTION="logfile"
    flyway.placeholders.VOLTMX_SERVER_SSL_SOCKETFACTORY_PROVIDER=
    com.ibm.websphere.ssl.protocol.SSLSocketFactory
    
    flyway.placeholders.VOLTMX_SERVER_SSL_SERVERSOCKETFACTORY_PROVIDER=
    com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
    flyway.placeholders.VOLTMX_SERVER_LOGGER_JNDI_NAME=jdbc/voltmxadmindb
    flyway.placeholders.VOLTMX_SERVER_SSL_SERVERSOCKETFACTORY_PROVIDER
    flyway.placeholders.VOLTMX_SERVER_SSL_SOCKETFACTORY_PROVIDER
    flyway.placeholders.VOLTMX_SERVER_LOG_OPTION 
        
    flyway.placeholders.SERVER_TOPIC_CONNECTION_FACTORY=ConnectionFactory
```

| No. | Property name | Place holder |
| ---| --- | --- |
| 1 | richclient.deploy | ${VOLTMX\_SERVER\_RICH\_CLIENT\_DEPLOY}<br><br> Example value, `lib/apps` (Directory where the rich client binaries will be downloaded. Used by admin module) |
| 2 | memcache.cluster | ${VOLTMX\_SERVER\_MEMCACHE\_CLUSTER}<br><br>Example value, `10.10.10.10:21201` ( where memcache cluster is running)<br><br>  **_Note:_** If the installation is being done without memcache, leave this value empty. |
| 3 | memcache.no.of.clients | ${VOLTMX\_SERVER\_MEMCACHED\_COUNT}<br><br>Example value, `1`<br><br>  **_Note:_** If the installation is being done without memcache, leave this value empty. |
| 4 | cacheid.transport | ${VOLTMX\_SERVER\_CACHEID\_TRANSPORT}<br><br>Example value, `Null`<br><br>(Specify the transfer mode through below property. Valid values are PARAM\_ONLY, COOKIE\_ONLY, EITHER (Default) or null if memcache is not used) |
| 5 | ssl.trustStore | ${VOLTMX\_SERVER\_TRUSTSTORE\_LOCATION}<br><br>Example value, `$JAVA_HOME/jre/lib/security/cacerts`<br><br>(cacerts Location) |
| 6 | ssl.keyStore | ${VOLTMX\_SERVER\_KEYSTORE\_LOCATION}<br><br>Example value, `$JAVA_HOME/jre/lib/security/cacerts`<br><br>(cacerts Location) |
| 7 | ssl.trustStorePassword | ${VOLTMX\_SERVER\_TRUSTSTORE\_PASSWORD}<br><br>Example value, `changeit` |
| 8 | ssl.keyStorePassword | ${VOLTMX\_SERVER\_TRUSTSTORE\_PASSWORD<br><br>Example value, `changeit` |
| 9 | metrics.initialContextFactoryName | ${VOLTMX\_SERVER\_JMS\_INITIAL\_CONTEXT\_FACTORY}<br><br>Example value,<br><br>i.    for WebLogic: `weblogic.jndi.WLInitialContextFactory`<br>ii.    for WebSphere: `com.ibm.websphere.naming.WsnInitialContextFactory`<br>iii.    for Tomcat: `org.apache.activemq.jndi.ActiveMQInitialContextFactory`<br>iv.    if jboss\_jms is used: `org.jboss.naming.remote.client.InitialContextFactory`<br>v.    if activemq is used: `org.apache.activemq.jndi.ActiveMQInitialContextFactory` |
| 10 | metrics.providerURL | ${VOLTMX\_SERVER\_JMS\_PROVIDER\_URL}<br><br>Example value,<br><br>For WebLogic: `t3://<ip>:<port>`<br>For WebSphere: `iiop://<ip>:<port>`<br>For Tomcat:  `tcp://$HOST_IP$:$USER_INPUT_JMS_PORT$?jms.useAsyncSend=TRUE`<br>For JBoss: `http-remoting://<Hostname/Host IP>:<HTTP Port>` |
| 11 | metrics.securityPrincipalName | ${VOLTMX\_SERVER\_JMS\_USER\_NAME},<br><br>Example value, `Weblogic`<br><br>(weblogic admin username) |
| 12 | metrics.securityCredentials | ${VOLTMX\_SERVER\_JMS\_USER\_PASSWORD}<br><br>Example value, `Weblogic123`<br><br>(weblogic admin password) |
| 13 | metrics.userName | ${VOLTMX\_SERVER\_JMS\_USER\_NAME}<br><br>Example value, `Weblogic`<br><br>(weblogic admin username) |
| 14 | metrics.password | ${VOLTMX\_SERVER\_JMS\_USER\_PASSWORD}<br><br>Example value, `Weblogic123`<br><br>(weblogic admin password) |
| 15 | SERVER\_LOG\_LOCATION | ${VOLTMX\_SERVER\_LOG\_LOCATION}<br><br>Example value, `C:/voltmxmflogs/`<br><br>(Log location for middleware log) |
| 16 | SERVER\_LOGGER\_JNDI\_NAME | ${VOLTMX\_SERVER\_LOGGER\_JNDI\_NAME}<br><br>Example value,`java:comp/env/jdbc/voltmxadmindb` |
        
  *   Tablespace Placeholders for **Oracle**:
        
         | Product Name | Tablespace Placeholders for Oracle |
         | --- | --- |
         | Admin DB / Integration Services | VOLTMX\_SERVER\_DATA\_TABLESPACE, VOLTMX\_SERVER\_INDEX\_TABLESPACE, VOLTMX\_SERVER\_LOB\_TABLESPACE |
        
  *   SQL files paths for an Admin in VoltMXFoundry\_Plugins folder:
        
         | Path for SQL files in the VoltMXFoundry\_Plugins folder | Database | Component |
         | --- | --- | --- |
         | \\VoltMXFoundry\_Plugins\\middleware\\admindb\_mysql | MySQL | Admin DB   |
         | \\VoltMXFoundry\_Plugins\\middleware\\admindb\_oracle | Oracle |
         | \\VoltMXFoundry\_Plugins\\middleware\\admindb\_sqlserver | SQL Server |
        
3.  Execute all SQL scripts by using the steps provided at [Configuring Flyway Command-line Tool](FlywayNew.md).
4.  Add the additional rows in the `server_configuration` table of `ADMINDB`. To add these rows, execute the following SQL query:
    
    insert into currentSchema.server\_configuration(prop\_name, prop\_value, created\_date , updated\_date) values(' management\_server\_host\_name, ‘server\_host\_ip/name ', CURRENT\_TIMESTAMP,CURRENT\_TIMESTAMP);  
    
    \# The following additional records will be inserted into the `server_configuration` table of the Admin DB:
    
    *   management\_server\_host\_name <AppServer\_host\_ip/name>
    *   management\_server\_port <AppServer\_port>  
          
        For Standalone JBoss the `management_server_port` should be `jboss.management.http.port`, which is present in the `standalone.xml` file.  
        
    *   management\_server\_user <AppServer\_username>
    *   management\_server\_password <AppServer\_encrypted password>
    *   management\_server\_groups <server\_groups>
    *   voltmx\_server\_shared\_lib\_name <name\_of\_the\_shared\_library\_created\_in\_websphere>_  
        (This property is required for WebSphere only_)
    *   management\_server\_scheme <http\_or\_https>
    *   server\_console\_redirect\_ip <Appserver\_host\_ip/name>_  
        (This property is required for JBoss domain mode only_)
    *   server\_console\_redirect\_port <Master\_Node HTTP/HTTPS Port>_  
        (This property is required for JBoss domain mode only_)
    *   management\_server\_truststore\_filename
    *   management\_server\_keystore\_filename
    *   management\_server\_truststore\_password
    *   management\_server\_keystore\_password
    *   cacheType = EHCACHE
    *   voltmxcentral.datasource = java:comp/env/jdbc/KDCDB

> **_Important:_** If you are installing Volt MX Foundry V8 on an application server using the existing database and in case if there is a change in server details, you must update the `management_server` details in the `admin` database with the application server instance details for the WebAapp publish to work. You must update the following fields in the `server_configuration` table of the **admin DB**:  
   \- management_server_host_name \<application_instance hostname\>  
   \- management_server_port \<soap port of application_instance\>  
   \- management_server_user \<application_instance admin username\>  
   \- management_server_password \<application_instance admin password\>  
   \- management_server_groups \<application_instance groups details\>

Click here to view the [Admin Server DB schema diagram](http://docs.voltmx.com/8_x_PDFs/MFSchema_Diagrams/admin_server.png)

Since the structure of flyway has changed from Flyway 3.2.1 to Flyway 4.0.3 in Volt MX Foundry installer, execute the following statements to make the `schema_version` table compatible with Flyway 4.0.3.

>**Oracle:**  
drop index "schema\_version\_ir\_idx";  
drop index "schema\_version\_vr\_idx";  
ALTER TABLE "schema\_version" DROP constraint "schema\_version\_pk" drop index;  
ALTER TABLE "schema\_version" DROP COLUMN "version\_rank";  
ALTER TABLE "schema\_version" modify("version" null);  
ALTER TABLE "schema\_version" add constraint "schema\_version\_pk" primary key("installed\_rank");  
  
>**MySQL:**  
ALTER TABLE schema\_version DROP INDEX schema\_version\_vr\_idx;  
ALTER TABLE schema\_version DROP INDEX schema\_version\_ir\_idx;  
ALTER TABLE schema\_version DROP PRIMARY KEY;  
ALTER TABLE schema\_version DROP COLUMN version\_rank;  
ALTER TABLE schema\_version CHANGE version version VARCHAR(50);  
ALTER TABLE schema\_version ADD PRIMARY KEY (installed\_rank);  
  
>**SQL Server:**  
DROP INDEX schema\_version\_ir\_idx ON dbo.schema\_version  
GO  
DROP INDEX schema\_version\_vr\_idx ON dbo.schema\_version  
GO  
ALTER TABLE dbo.schema\_version DROP CONSTRAINT schema\_version\_pk  
GO  
ALTER TABLE dbo.schema\_version DROP COLUMN version\_rank  
GO  
ALTER TABLE dbo.schema\_version ADD CONSTRAINT schema\_version\_pk PRIMARY KEY CLUSTERED (installed\_rank)  
GO  
ALTER TABLE dbo.schema\_version ALTER COLUMN version nvarchar(50) NULL  
GO -->



## Create and Configure a Database for **VoltMX Admin**

To create a database for **Admin**, follow these steps:

1.  Create a database for admin with a custom name along with prefix and suffix. Prefix and suffix are optional. For example, database name is `<prefix>admindb<suffix>`.

    > **_Note:_**  For Oracle databases, a schema name should be in capital letters.  
    >  Find the word `adminDB` in SQL files located in the admin scripts and replace it with `ADMINDB`.

    > **_Note:_** For Oracle, create necessary tablespaces and Users before proceeding. Refer to [Prerequisites for Volt MX Foundry with Oracle](Database_Prerequsites.md#prerequisites-for-volt-mx-foundry-with-oracle).

    Volt MX

    **The following is a sample query for creating a database in MSSQL:**

    `CREATE DATABASE admindb;`

    The following is a sample query for creating a database in MySQL:

    <code>CREATE DATABASE &lt;DBNAME&gt; DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;</code>

2.  The following details are required for Flyway configuration:

    - Schema name for Admin: `admindb`
    - Placeholders for Admin:

### For Admin (admindb):

replace the following placeholders in SQL migrations for your database flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_TYPE -> value must be

```
    mysql/oracle/sqlserver based on the chosen databases.

    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_HOSTNAME -> database host name where
    admindb is created.

    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_PORT -> database port where
    admindb is created.

    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_USERNAME -> database user name
    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_PASSWORD ->:  ([Encrypt](Encrypt_Passwords.md) this password)
          - For MySQL and SQL Server: database user password

    flyway.placeholders.VOLTMX_SERVER_STORAGE_DATABASE_INSTANCE ->  MySQL – empty,
    SQL Server – instance name if given, Oracle - SID name. flyway.placeholders.VOLTMX_SERVER_CACHEID_TRANSPORT=""flyway.placeholders.VOLTMX_SERVER_SESSION_DISTRIBUTED="FALSE"
    flyway.placeholders.VOLTMX_SERVER_CACHE_TYPE="EHCACHE"
    flyway.placeholders.VOLTMX_SERVER_CACHE_URL="" flyway.placeholders.VOLTMX_SERVER_JMS_INITIAL_CONTEXT_FACTORY=""
    flyway.placeholders.VOLTMX_SERVER_JMS_PROVIDER_URL=""
    flyway.placeholders.VOLTMX_SERVER_JMS_USER_NAME=""
    flyway.placeholders.VOLTMX_SERVER_JMS_USER_PASSWORD="" ([Encrypt](Encrypt_Passwords.md) this password) flyway.placeholders.VOLTMX_SERVER_KEYSTORE_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_LOG_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_MEMCACHED_COUNT=""
    flyway.placeholders.VOLTMX_SERVER_MEMCACHE_CLUSTER=""
    flyway.placeholders.VOLTMX_SERVER_RICH_CLIENT_DEPLOY=""
    flyway.placeholders.VOLTMX_SERVER_TRUSTSTORE_LOCATION=""
    flyway.placeholders.VOLTMX_SERVER_TRUSTSTORE_PASSWORD=""  ([Encrypt](Encrypt_Passwords.md) this password)
    flyway.placeholders.VOLTMX_SERVER_LOG_OPTION="logfile"
    flyway.placeholders.VOLTMX_SERVER_SSL_SOCKETFACTORY_PROVIDER=
    com.ibm.websphere.ssl.protocol.SSLSocketFactory

    flyway.placeholders.VOLTMX_SERVER_SSL_SERVERSOCKETFACTORY_PROVIDER=
    com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
    flyway.placeholders.VOLTMX_SERVER_LOGGER_JNDI_NAME=jdbc/voltmxadmindb
    flyway.placeholders.VOLTMX_SERVER_SSL_SERVERSOCKETFACTORY_PROVIDER
    flyway.placeholders.VOLTMX_SERVER_SSL_SOCKETFACTORY_PROVIDER
    flyway.placeholders.VOLTMX_SERVER_LOG_OPTION

    flyway.placeholders.SERVER_TOPIC_CONNECTION_FACTORY=ConnectionFactory
```

| No. | Property name                     | Place holder                                                                                                                                                                                                                                                                                                                                                                                          |
| --- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | richclient.deploy                 | ${VOLTMX_SERVER_RICH_CLIENT_DEPLOY}<br><br> Example value, `lib/apps` (Directory where the rich client binaries will be downloaded. Used by admin module)                                                                                                                                                                                                                                             |
| 2   | memcache.cluster                  | ${VOLTMX_SERVER_MEMCACHE_CLUSTER}<br><br>Example value, `10.10.10.10:21201` ( where memcache cluster is running)<br><br> **_Note:_** If the installation is being done without memcache, leave this value empty.                                                                                                                                                                                      |
| 3   | memcache.no.of.clients            | ${VOLTMX_SERVER_MEMCACHED_COUNT}<br><br>Example value, `1`<br><br> **_Note:_** If the installation is being done without memcache, leave this value empty.                                                                                                                                                                                                                                            |
| 4   | cacheid.transport                 | ${VOLTMX_SERVER_CACHEID_TRANSPORT}<br><br>Example value, `Null`<br><br>(Specify the transfer mode through below property. Valid values are PARAM_ONLY, COOKIE_ONLY, EITHER (Default) or null if memcache is not used)                                                                                                                                                                                 |
| 5   | ssl.trustStore                    | ${VOLTMX\_SERVER\_TRUSTSTORE\_LOCATION}<br><br>Example value, `$JAVA_HOME/jre/lib/security/cacerts`<br><br>(cacerts Location)                                                                                                                                                                                                                                                                         |
| 6   | ssl.keyStore                      | ${VOLTMX\_SERVER\_KEYSTORE\_LOCATION}<br><br>Example value, `$JAVA_HOME/jre/lib/security/cacerts`<br><br>(cacerts Location)                                                                                                                                                                                                                                                                           |
| 7   | ssl.trustStorePassword            | ${VOLTMX_SERVER_TRUSTSTORE_PASSWORD}<br><br>Example value, `changeit`                                                                                                                                                                                                                                                                                                                                 |
| 8   | ssl.keyStorePassword              | ${VOLTMX_SERVER_TRUSTSTORE_PASSWORD<br><br>Example value, `changeit`                                                                                                                                                                                                                                                                                                                                  |
| 9   | metrics.initialContextFactoryName | ${VOLTMX_SERVER_JMS_INITIAL_CONTEXT_FACTORY}<br><br>Example value,<br><br>ii. for WebSphere: `com.ibm.websphere.naming.WsnInitialContextFactory`<br>iii. for Tomcat: `org.apache.activemq.jndi.ActiveMQInitialContextFactory`<br>iv. if jboss_jms is used: `org.jboss.naming.remote.client.InitialContextFactory`<br>v. if activemq is used: `org.apache.activemq.jndi.ActiveMQInitialContextFactory` |
| 10  | metrics.providerURL               | ${VOLTMX\_SERVER\_JMS\_PROVIDER\_URL}<br><br>Example value,<br><br>For Tomcat:  `tcp://$HOST_IP$:$USER_INPUT_JMS_PORT$?jms.useAsyncSend=TRUE`<br>For JBoss: `http-remoting://<Hostname/Host IP>:<HTTP Port>`                                                                                                                                                                                          |
| 11  | SERVER_LOG_LOCATION               | ${VOLTMX_SERVER_LOG_LOCATION}<br><br>Example value, `C:/voltmxmflogs/`<br><br>(Log location for middleware log)                                                                                                                                                                                                                                                                                       |
| 12  | SERVER_LOGGER_JNDI_NAME           | ${VOLTMX_SERVER_LOGGER_JNDI_NAME}<br><br>Example value,`java:comp/env/jdbc/voltmxadmindb`                                                                                                                                                                                                                                                                                                             |


- Tablespace Placeholders for **Oracle**:

  | Product Name                    | Tablespace Placeholders for Oracle                                                          |
  | ------------------------------- | ------------------------------------------------------------------------------------------- |
  | Admin DB / Integration Services | VOLTMX_SERVER_DATA_TABLESPACE, VOLTMX_SERVER_INDEX_TABLESPACE, VOLTMX_SERVER_LOB_TABLESPACE |

- SQL files paths for an Admin in VoltMXFoundry_Plugins folder:

  | Path for SQL files in the VoltMXFoundry_Plugins folder | Database   | Component  |
  | ------------------------------------------------------ | ---------- | ---------- |
  | \\VoltMXFoundry_Plugins\\middleware\\admindb_mysql     | MySQL      | Admin DB   |
  | \\VoltMXFoundry_Plugins\\middleware\\admindb_oracle    | Oracle     |
  | \\VoltMXFoundry_Plugins\\middleware\\admindb_sqlserver | SQL Server |


3.  Execute all SQL scripts by using the steps provided at [Configuring Flyway Command-line Tool](FlywayNew.md).

4.  Add the additional rows in the `server_configuration` table of `ADMINDB`. To add these rows, execute the following SQL query:

    insert into currentSchema.server_configuration(prop_name, prop_value, created_date , updated_date) values(' management_server_host_name, ‘server_host_ip/name ', CURRENT_TIMESTAMP,CURRENT_TIMESTAMP);

    \# The following additional records will be inserted into the `server_configuration` table of the Admin DB:

    - management_server_host_name <AppServer_host_ip/name>
    - management_server_port <AppServer_port>
      For Standalone JBoss the `management_server_port` should be `jboss.management.http.port`, which is present in the `standalone.xml` file.
    - management_server_user <AppServer_username>
    - management_server_password <AppServer_encrypted password>
    - management_server_groups <server_groups>
    - voltmx_server_shared_lib_name <name_of_the_shared_library_created_in_websphere>_  
      (This property is required for WebSphere only_)
    - management_server_scheme <http_or_https>
    - server_console_redirect_ip <Appserver_host_ip/name>_  
      (This property is required for JBoss domain mode only_)
    - server_console_redirect_port <Master_Node HTTP/HTTPS Port>_  
      (This property is required for JBoss domain mode only_)
    - management_server_truststore_filename
    - management_server_keystore_filename
    - management_server_truststore_password
    - management_server_keystore_password
    - cacheType = EHCACHE
    - voltmxcentral.datasource = java:comp/env/jdbc/KDCDB

> **_Important:_** If you are installing Volt MX Foundry V8 on an application server using the existing database and in case if there is a change in server details, you must update the `management_server` details in the `admin` database with the application server instance details for the WebAapp publish to work. You must update the following fields in the `server_configuration` table of the **admin DB**:  
>  \- management_server_host_name \<application_instance hostname\>  
>  \- management_server_port \<soap port of application_instance\>  
>  \- management_server_user \<application_instance admin username\>  
>  \- management_server_password \<application_instance admin password\>  
>  \- management_server_groups \<application_instance groups details\>

Click here to view the [Admin Server DB schema diagram](http://docs.voltmx.com/8_x_PDFs/MFSchema_Diagrams/admin_server.png)

Since the structure of flyway has changed from Flyway 3.2.1 to Flyway 4.0.3 in Volt MX Foundry installer, execute the following statements to make the `schema_version` table compatible with Flyway 4.0.3.

> **Oracle:**  
> drop index "schema_version_ir_idx";  
> drop index "schema_version_vr_idx";  
> ALTER TABLE "schema_version" DROP constraint "schema_version_pk" drop index;  
> ALTER TABLE "schema_version" DROP COLUMN "version_rank";  
> ALTER TABLE "schema_version" modify("version" null);  
> ALTER TABLE "schema_version" add constraint "schema_version_pk" primary key("installed_rank");

> **MySQL:**  
> ALTER TABLE schema_version DROP INDEX schema_version_vr_idx;  
> ALTER TABLE schema_version DROP INDEX schema_version_ir_idx;  
> ALTER TABLE schema_version DROP PRIMARY KEY;  
> ALTER TABLE schema_version DROP COLUMN version_rank;  
> ALTER TABLE schema_version CHANGE version version VARCHAR(50);  
> ALTER TABLE schema_version ADD PRIMARY KEY (installed_rank);

> **SQL Server:**  
> DROP INDEX schema_version_ir_idx ON dbo.schema_version  
> GO  
> DROP INDEX schema_version_vr_idx ON dbo.schema_version  
> GO  
> ALTER TABLE dbo.schema_version DROP CONSTRAINT schema_version_pk  
> GO  
> ALTER TABLE dbo.schema_version DROP COLUMN version_rank  
> GO  
> ALTER TABLE dbo.schema_version ADD CONSTRAINT schema_version_pk PRIMARY KEY CLUSTERED (installed_rank)  
> GO  
> ALTER TABLE dbo.schema_version ALTER COLUMN version nvarchar(50) NULL  
> GO


