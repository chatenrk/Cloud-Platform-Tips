# Cloud Platform Services

- [Cloud Platform Services](#cloud-platform-services)
  - [Procedure to setup Cloud Platform Service](#procedure-to-setup-cloud-platform-service)
  - [Service Instance Parameters](#service-instance-parameters)
  - [Services Setup](#services-setup)
    - [Authorization & Trust Management](#authorization--trust-management)
    - [Destination](#destination)

## Procedure to setup Cloud Platform Service
Select the "Service Marketplace" menu item (within the "Services" item in the menu on the left hand side)

![Service Marketplace](./screenshots/service-marketplace.png)

Select the service from the Service Marketplace
![Service Marketplace 2](./screenshots/service-marketplace2.png)

Click the new instance button
![Service Marketplace 3](./screenshots/copy%20-service-marketplace3.png)

## Service Instance Parameters
| Service                          | Technical Name | Service Plan  | Parameters                                                 | Assign Application | Instance Name      |
| -------------------------------- | -------------- | ------------- | ---------------------------------------------------------- | ------------------ | ------------------ |
| Authorization & Trust Management | `xsuaa`        | `application` | Upload the `xs-security.json` file via the "Browse" button | (none)             | `test-xsuaa`       |
| Destination                      | `destination`  | `lite`        | (none)                                                     | (none)             | `test-destination` |

## Services Setup
### Authorization & Trust Management
To create an Authorization & Trust Management service select the same in Service Marketplace and create a new instance as show below
![XSUAA](./screenshots/XSUAA/service.png)
![XSUAA 1](./screenshots/XSUAA/service1.png)
![XSUAA 3](./screenshots/XSUAA/service3.png)
![XSUAA 4](./screenshots/XSUAA/service4.png)
![XSUAA 5](./screenshots/XSUAA/service5.png)
![XSUAA 6](./screenshots/XSUAA/service6.png)
### Destination
To create a Destination service select the same in Service Marketplace and create a new instance as show below
![Destination](./screenshots/Destination/service.png)
![Destination 2](./screenshots/Destination/service2.png)
![Destination 3](./screenshots/Destination/service3.png)
![Destination 4](./screenshots/Destination/service4.png)
![Destination 5](./screenshots/Destination/service5.png)
![Destination 6](./screenshots/Destination/service6.png)