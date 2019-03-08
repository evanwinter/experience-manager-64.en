---
title: Global document storage directory
seo-title: Global document storage directory
description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 50b1e061-e667-4704-9e16-d626a55c0cc5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9253a14e-9c7c-4aed-8241-8b7a2bdc0a6f
index: y
internal: n
snippet: y
---

# Global document storage directory{#global-document-storage-directory}

The *global document storage (GDS)* directory is a directory used to store long-lived files that are used within a process. These files include PDFs, policies, and form templates. Long-lived files are a critical part of the overall state of many AEM forms deployments. If some or all long-lived documents are lost or corrupted, the forms server may become unstable. Input documents for asynchronous job invocations are also stored in the GDS directory and must be available to process requests. It is important that you consider the reliability of the file system that hosts the GDS directory. User a redundant array of independent disks (RAID) or other technology as appropriate for your quality and level of service needs.

Long-lived files may contain sensitive user information. This information may require special credentials when accessed by using the AEM forms APIs or user interfaces. It is important that the GDS directory is properly secured through the operating system. Only the administrator account that is used to run the application server should have read/write access to the GDS directory.

In addition to selecting a secure, highly available directory for GDS, you can also choose to enable document storage in the database. Notice that even with using the AEM forms database for document storage, AEM forms still requires the GDS directory. (See [Backup options when database is used for document storage](../../../forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms application data resides in the GDS directory and the AEM forms database. The following table describes the data and its locations.

<table cellpadding="4" cellspacing="0"> 
 <thead align="left"> 
  <tr> 
   <th class="cellrowborder" id="d19e29288" valign="top" width="NaN%"><p>AEM forms Data</p></th> 
   <th class="cellrowborder" id="d19e29291" valign="top" width="NaN%"><p>Database</p></th> 
   <th class="cellrowborder" id="d19e29294" valign="top" width="NaN%"><p>GDS</p></th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>Application data (users, roles, processes, policies, endpoints, events, and so on.)</p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>Yes</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>No</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>Deployed service containers</p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>Yes</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>No</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>Document Manager </p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>No</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>Yes</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>Forms Repository</p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>Yes</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>No</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>System configuration</p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>Yes</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>No</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e29288 " valign="top" width="NaN%"><p>Watched folders</p></td> 
   <td class="cellrowborder" headers="d19e29291 " valign="top" width="NaN%"><p>No</p></td> 
   <td class="cellrowborder" headers="d19e29294 " valign="top" width="NaN%"><p>Yes</p></td> 
  </tr> 
 </tbody> 
</table>

## Configuring the GDS directory {#configuring-the-gds-directory}

The location of the GDS directory can be configured manually during the AEM forms installation process. If the location setting remains empty during installation, the location defaults to a directory under the application server installation as follows:

* (JBoss) *[appserver root]*/server/*[type]*/svcnative/DocumentStorage
* (WebLogic) *[appserverdomain]*/*[server]*/adobe/DocumentServer/DocumentStorage
* (WebSphere) *[appserver root]*/installedApps/adobe/*[server]*/DocumentStorage

## Change the default GDS location {#change-the-default-gds-location}

You can change the GDS location in administration console after the AEM forms installation is completed. You must manually relocate the data to complete the process.

>[!NOTE]
>
>Migrate the data in the following manner or data loss will occur.

1. Log in to administration console and click Settings &gt; Core System Settings &gt; Configurations.
1. In the Global Document Storage Directory box, enter the full path to the new GDS directory and then click OK.
1. Immediately shut down the application server.
1. Move all the files from the old GDS directory to the new location, keeping the internal directory structure. 
1. Restart the application server.

## About Deployment Files {#about-deployment-files}

AEM forms consists of two types of deployment files, the service containers and the Java 2 Platform, Enterprise Edition (J2EE) EAR files. The EAR files consist of standard J2EE application bundles that contain the core functionality of AEM forms. The application server-specific EAR files are as follows:

* adobe-core-*[appserver]*.ear 
* adobe-core-*[appserver]*-*[OS]*.ear

Implementing AEM forms involves deploying the assembled EAR files and supporting files to the application server where you plan to run your AEM forms solution. If you configured and assembled multiple modules, the deployable modules are packaged within the deployable EAR files. To deploy these files, copy them to the *[appserver home]*\server\all\deploy directory.

Modules and AEM forms archive files are packaged in JAR files. Because they are not J2EE type files, they are not deployed to the application server. Instead, they are copied into the GDS directory, and a reference to their location is stored in the AEM forms database. For this reason, the GDS directory must be shared among all the nodes of the cluster. All the nodes must have access to the central storage directory for the DSCs.

>[!NOTE]
>
>Before you deploy the service containers, ensure that you created and configured the GDS directory. (See [Configuring the GDS directory](global-document-storage-directory.md#configuring_the_gds_directory))
