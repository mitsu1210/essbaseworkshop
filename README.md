# Introduction to Essbase

## Introduction

Oracle Essbase is a business analytics solution that uses a proven, flexible, best-in-class architecture for analysis, reporting, and collaboration. Essbase delivers instant value and greater productivity for your business users, analysts, modelers, and decision-makers, across all lines of business within your organization.

Oracle Essbase on cloud helps you to build your company’s cloud strategy efficiently by avoiding data and business process fragmentation. Oracle Essbase can be easily deployed on Oracle Cloud Infrastructure, which can then be widely used to solve simple to complex business analytics use cases across all industries. It is designed to help you model business performance levels and deliver what-if analyses for varying conditions. Using Oracle Identity Cloud Service, Essbase can utilize enterprise-wide user profiles to work and integrate with Oracle Cloud.

## Features of Oracle Essbase

•	Oracle Essbase provides a complete set of tools and features for deriving and sharing data insights.

•	Both large organizations and small teams can share data more simply, without the need to manage or consolidate multiple versions of spreadsheets, and quickly perform ad hoc analysis of the spreadsheet data.

•	Application developers can utilize interfaces that enable them to extend, customize, and embed rich analytic experiences in the application flow.

•	With Oracle Essbase, you can take data from any source, and explore and collaborate with real-time data, using a               multidimensional engine.

•	With Essbase on cloud you can create and manage Essbase applications from Microsoft Excel by using Cube Designer.

•	Create connections and data sources for drill-through, data loads, and dimension builds.

•	We can use Essbase to collect collaborative data, create scenarios, and perform what-if analysis using Smart View.

## Essbase on OCI – Essbase 19c 

The following diagram shows Essbase 19c deployed on Oracle infrastructure cloud (OCI) with integration to different cloud services - Autonomous Database, Load Balancer, Storage, Virtual Cloud Network (VCN) as part of the deployment.

Attached below is a generic sample architecture:
![](Architecture.png)

* Essbase19c VM resides in the Application subnet as shown in the above figure which is configured automatically with Block Volumes – Configuration Volume & Data Volume. 

* The connections to this application subnet are dependent on the Security List rules associated with the Application subnet. In this topology we will have ingress rules on the application subnet for SSH Connectivity and for HTTPS - Web UI connectivity to the Essbase19c VM via the Internet Gateway.

* SSH connectivity is first required during the procurement process for the Resource Manager to configure & install the Essbase19c in the compute instance automatically with no manual work from our end and secondly after the procurement SSH connectivity enables the users to login to the backend Essbase19c instance and for corresponding access.

* The Essbase19c instance procured will manage its users using the IDCS of Oracle Cloud & metadata gets stored in the ATP-Autonomous Database.

* Essbase backups gets stored in the Object storage of the OCI & the connectivity to this is established by the service gateway.


*Note:* This lab is intended to be a comprehensive full cloud showcase. As such, it is assumed a user going through this workshop will be provisioning resources and creating users from scratch. If you decide to use existing infrastructure or resources, be aware and keep note of your namings so resources don't overlap and conflict.

*Note:* Additionally, as much as possible, do not stray away from the naming conventions used for resources in this worshop. You may run into errors if you do.

## Working with Essbase


### Required Artifacts

•	The following lab requires an Oracle Public Cloud account that will either be supplied by your instructor, or can be obtained through the following steps.
•	A cloud tenancy where you have the resources available to provision an ADW instance with 2 OCPUs, an Essbase instance with 2 OCPUs
•	Smartview Plugin
•	Cube Designer Plugin


## Register for Free Oracle Trial Account
* Bookmark this page for future reference.
* Please click on the URL to receive your [Free Account](https://myservices.us.oraclecloud.com/mycloud/signup?language=en&sourceType=:ex:tb:::RC_NAMK190227P00084:PredictDemandML_ADW_HOL&SC=:ex:tb:::RC_NAMK190227P00084:PredictDemandML_ADW_HOL&pcode=NAMK190227P00084) and complete all required steps. When you complete the registration process you'll receive a $300 credit that will enable you to complete the lab for free. Additionally, you'll have 1000s of hours left over to continue to explore the Oracle Cloud.
* Soon after requesting your trial you will receive an activation email. Once that email is received and you have logged in to your environment you can begind the lab.

Access the labs using our web-friendly interface [here](https://bangaloresolutionshub.github.io/essbaseworkshop/)  
