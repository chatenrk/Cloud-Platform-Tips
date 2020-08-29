# Provision Hana Cloud on SAP Cloud Platform

- [Provision Hana Cloud on SAP Cloud Platform](#provision-hana-cloud-on-sap-cloud-platform)
  - [Setup CP Trail Account](#setup-cp-trail-account)
  - [Check Entitlements](#check-entitlements)
  - [Create Instance of Hana Cloud](#create-instance-of-hana-cloud)
  - [Import SFLIGHT Schema](#import-sflight-schema)

## Setup CP Trail Account
For information related to creating a new SAP Cloud Platform account refer to the [section](../../Setup%20CP%20trial/readme.md)

## Check Entitlements
Check entitlements are available as expected
![Check Entitlements](screenshots/check-entitlements.png)

## Create Instance of Hana Cloud
Create an instance as shown below
![Provision Hana Cloud 1](screenshots/provision-hana-cloud1.png)
![Provision Hana Cloud 2](screenshots/provision-hana-cloud2.png)
![Provision Hana Cloud 3](screenshots/provision-hana-cloud3.png)
![Provision Hana Cloud 4](screenshots/provision-hana-cloud4.png)
![Provision Hana Cloud 5](screenshots/provision-hana-cloud5.png)

New Hana Cloud Instance is created
![New Hana Instance](screenshots/new-instance.png)

Open database explorer(check hana-cli [shortcut](../../../README.md#hana-cli-related)) and add the new database instance
![Database Explorer](screenshots/database-explorer.png)

## Import SFLIGHT Schema
Download SFLIGHT from [SAP Samples](https://github.com/SAP/hana-xsa-opensap-hana7/raw/snippets_2.3.2/ex2/sflight_hana.tar.gz) GITHUB repository. Once it is saved locally, right-click on the database created above and click Import Catalog Objects
![Sflight 1](screenshots/sflight1.png)
Browse and import the file
![Sflight 2](screenshots/sflight2.png)
Schema is created, and all relevant objects are imported
![Sflight3](screenshots/sflight3.png)




