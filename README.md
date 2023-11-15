# ReadMe.md

## Overview

Organizations leveraging the Center of Excellence Toolkit from Microsoft often employ data governance processes built on the insights provided by the toolkit. However, the toolkit is a starter solution and at times requires additional build-out for unique governance requirements by a respective organization.

Data governance is key to the Power Platform as Connectors and On-prem Data Gateways allow for powerful yet complex data flows across the technology landscape. One of the major requirements that has continuously arose is the need to see which Apps and Flows are using what On-prem Data Gateways and what on-prem data sources. This solution augments an already installed Center of Excellence Toolkit by tagging Connections to the respective On-prem Data Gateway.

## Security Roles Required

For installation and configuration of the solution, the following security roles are required:

Office 365 Security Role: Power Platform Admin or Global Administrator

For using the Data Governance App, the user must be assigned the custom role contained in the solution:

Data Governance Power Platform User SR

## License Requirements

For installation of the solution, the following license types are required:

- Power Apps Premium
- Power Automate Premium

To run the Data Governance apps, the following license types are required:

- Power Apps Premium

## Installing the Solution

### Environment

This solution must be installed in the environment where the Center of Excellence Toolkit is installed. At least the Core Component solutions must be installed. For more information, see the installation instructions for the toolkit here: [Set up inventory components - Power Platform | Microsoft Learn](https://learn.microsoft.com/en-us/power-platform/guidance/coe/setup-core-components)

### Import Solution

1. Download the solution from the [latest release.](https://github.com/v7herman4/COE-Toolkit-Data-Governance/releases)
2. In the Power Platform maker experience, navigate to the target environment and import the solution.

## Configure the Data Governance App

### Add On-prem Data Gateway Records

The COE toolkit data set does not contain any records that hold information on the On-Prem Data Gateways. Therefore they must be added manually to the Data Governance App.

Navigate to the Power Platform Admin Center. Click on _Data_, click on _On-premises data gateways_, click on _Tenant administration for gateways_.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/1f154260-cef5-4dc5-8104-412d81053199)

For each gateway, hover over the record and click the information circle. Add the gateway name and the gateway id in a spreadsheet or text file.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/43d1b2c6-77c0-4cce-9adb-d39cb649199e)


From the Data Governance app, export a blank spreadsheet, update the spreadsheet with the On-prem Data Gateway information and then upload back into the table.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/3cfe31ca-550d-4a79-944d-c2223e25074b)

## Run the _Update Connection Refs with Gateway Info_ Flow

The _Update Connection Refs with Gateway Info_ Flow runs on a nightly basis. Update the trigger to run as often as required.

## How to Use the Data Governance App

### Connection References

The Connection References areas shows all Apps and Flows that contain a Connection which uses an On-prem Data Gateway. The associated App or Flow is displayed as well as the Data Gateway, the SQL Server Name and the SQL Server database.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/c78f21d5-7856-47b4-aeaa-43bc2cfeb900)

### Apps with Data Gateway Connections

The Apps shows all Apps that contain a Connection which uses an On-prem Data Gateway AND is shared with at least one other user beside the Owner. The associated App is displayed as well as the number of users or groups its shared with, the Data Gateway, the SQL Server Name and the SQL Server database.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/6339d0c8-6458-49e9-8825-4d4ff10dd6ce)

### Flows with Data Gateway Connections

The Flows area shows all Flows that contain a Connection which uses an On-prem Data Gateway AND is shared with at least one other user beside the Owner. The associated Flow is displayed as well as the number of users or groups its shared with, the Data Gateway, the SQL Server Name and the SQL Server database.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/6744f3ef-cef8-452b-afc3-7d695b26e69e)

## FAQ

### How does the Data Governance Solution identify Apps or Flows with Connections tied to a Data Gateway?

Key to the Data Governance Solution is the ability of the Power Platform Admin connectors to retrieve all Connections in an Environment using the _Get Connections as Admin_ action. The resulting json contains Connection information including the Data Gateway Id.

![image](https://github.com/v7herman4/COE-Toolkit-Data-Governance/assets/89024016/d720f416-1483-4032-b258-e6d21d941874)

Using the additional Admin Connector actions such as _Get Apps as Admin_ and _List flows as Admin (V2)_ the Power Automate Flow can identify which Apps and Flows are using the Connections highlighted. Parsing of the raw json as an output of the action is required as opposed to using the out of the box values returned.

The Power Automate Flow will update the existing Connection Reference record with the Data Gateway Id and SQL Server information identified.

![](RackMultipart20231115-1-bogat7_html_a1bc3af9b93731bc.png)
