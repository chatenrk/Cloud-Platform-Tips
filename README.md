# SAP Cloud Platform Tips and Tricks

**[Table of Contents]**

- [Cloud Platform Setup](https://github.com/chatenrk/Cloud-Platform-Tips/blob/master/Cloud%20Platform%20related/readme.md)
- [Quick Access Commands](#quick-access-commands)
  - [CF CLI Related](#cf-cli-related)
  - [HANA CLI Related](#hana-cli-related)
  - [Github Related]()
- [SQL Commands](#sql-commands)
- [XSA Quick references](#xsa-quick-references)
- [CF-CLI Tips](#cf-cli-tips)
- [Bash Terminal Tips](https://github.com/chatenrk/Cloud-Platform-Tips/blob/cleanUpGit/Bash%20Terminal%20Tips/readme.md)

## Quick Access Commands

### CF CLI Related

| Description                  | Command                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Help for CF CLI              | `cf --help (or) cf -h`                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Login to cloud foundry       | `cf login (or) cf l`                                                                                                                                                                                                                                                                                                                                                                                                                         |
| List all services            | `cf services (or) cf s`                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Create service               | `cf create-service SERVICE PLAN SERVICE_INSTANCE [-b BROKER] [-c PARAMETERS_AS_JSON] [-t TAGS]` <br> **where** <br> - SERVICE_INSTANCE is the name of service instance which needs to be created <br> - CREDENTIALS is a JSON object, sample JSON as below <br> **Example** <br> `cf create-service hana hana-shared test-hana-service`                                                                                                      |
| Create Service Key           | `cf create-service-key SERVICE_INSTANCE SERVICE_KEY [-c PARAMETERS_AS_JSON]` <br> **where** <br> - SERVICE_INSTANCE is the name of service instance which was created above <br> - SERVICE_KEY is the name of the service key <br> **Example** <br> `cf create-service-key test-hana-service default`                                                                                                                                        |
| Create User Provided Service | `cf create-user-provided-service SERVICE_INSTANCE [-p CREDENTIALS] [-l SYSLOG_DRAIN_URL] [-r ROUTE_SERVICE_URL] [ -t TAGS]` <br> **where** <br> - SERVICE_INSTANCE is the name of service instance which needs to be created <br> - CREDENTIALS is a JSON object, sample JSON as below <br> `{\"user\":\"CUPS_SFLIGHT\",\"password\":\"<Password>\",\"driver\":\"com.sap.db.jdbc.Driver\",\"tags\":[\"hana\"] , \"schema\" : \"SFLIGHT\" }"` |

### HANA CLI Related

| Description                                                 | Command                                                                                                                                                                                                               |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HANA CLI Help                                               | `hana-cli help`                                                                                                                                                                                                       |
| HANA CLI Connect                                            | `hana-cli connect`                                                                                                                                                                                                    |
| Open database explorer                                      | `hana-cli opendbx`                                                                                                                                                                                                    |
| Check status of Hana Database                               | `hana-cli status`                                                                                                                                                                                                     |
| Connect ServiceKey and service and prepare default-env.json | `hana-cli serviceKey [instance] [key]` <br> **where** <br> - instance is the name of the hana service instance created in cloud platform(via CLI or directly) <br> - key is the service created for the above service |
| Inspect a table                                             | `hana-cli inspectTable <<Insert Schema Name>> <<Insert Table Name>>`                                                                                                                                                  |
| Generate CDS from existing table                            | `hana-cli inspectTable <<Insert Schema Name>> <<Insert Table Name>> -o cds`                                                                                                                                           |

## SQL Commands

| Description                 | Command                                                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create user                 | ` CREATE USER CUPS_SFLIGHT PASSWORD "<Password>" SET PARAMETER CLIENT = '001' SET USERGROUP DEFAULT;`                                                                     |
| Disable password            | `ALTER USER CUPS_SFLIGHT DISABLE PASSWORD LIFETIME`                                                                                                                       |
| Grant Schema to User        | `GRANT SELECT ON SCHEMA SFLIGHT TO CUPS_SFLIGHT WITH GRANT OPTION;` <br> `GRANT SELECT METADATA ON SCHEMA SFLIGHT to CUPS_SFLIGHT WITH GRANT OPTION;`                     |
| Create Role                 | `CREATE ROLE SFLIGHT_CONTAINER_ACCESS;`                                                                                                                                   |
| Grant Schema to Role & User | `GRANT SELECT, SELECT METADATA ON SCHEMA SFLIGHT TO SFLIGHT_CONTAINER_ACCESS WITH GRANT OPTION;` <br> `GRANT SFLIGHT_CONTAINER_ACCESS TO CUPS_SFLIGHT WITH ADMIN OPTION;` |

## XSA Quick references

### Add resource to MTA.YAML

Use the below sample code to add a new resource to MTA.YAML. This is helpful to add User provided services to an MTA Application

- **Existing Service**

```shell
  # ------------------------------------------------------------
  - name: <insert name of service>
    # ------------------------------------------------------------
    type: org.cloudfoundry.existing-service
    parameters:
      service-name: <name of service existing on cloud platform >
    properties:
      ServiceName_1: "${service-name}"
```

### Add UPS to default-env.json

```shell
"user-provided": [
            {
                "label": "user-provided",
                "name": "CROSS_SCHEMA_SFLIGHT",
                "tags": [],
                "instance_name": "CROSS_SCHEMA_SFLIGHT",
                "binding_name": null,
                "credentials": {
                    "password": "HanaRocks01",
                    "schema": "SFLIGHT",
                    "tags": [
                        "hana"
                    ],
                    "user": "CUPS_SFLIGHT"
                },
                "syslog_drain_url": "",
                "volume_mounts": []
            }
        ]
```

### Add Service replacements to UPS

```s
"SERVICE_REPLACEMENTS": [
        {
            "key": "ServiceName_1",
            "service": "CROSS_SCHEMA_SFLIGHT"
        }
    ]
```
