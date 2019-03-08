---
title: Optimizing HTML5 forms
seo-title: Optimizing HTML5 forms
description: You can optimize the output size of the HTML5 forms.
seo-description: You can optimize the output size of the HTML5 forms.
uuid: dc28fc88-d1e9-4cb3-a3ae-08f174030311
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: dce049b6-8f9d-42ce-9752-143c8a4e6f5b
index: y
internal: n
snippet: y
---

# Optimizing HTML5 forms{#optimizing-html-forms}

HTML5 forms renders forms in the HTML5 format. The resultant output could be large depending on factors like the form size and images in the form. To optimize the data transfer, the recommended approach is to compress the HTML response using the Web Server from which the request is being served. This approach reduces the response size, network traffic, and the time required to stream data between the server and client machines.

This article describes the steps required to enable compression for the Apache Web Server 2.0 32 bit, with JBoss.

*Note: The following instructions do not apply to server other than the Apache Web Server 2.0 32 bit. *

Obtain the Apache web server software applicable to your operating system:

* For Windows, download the Apache web server from the Apache HTTP Server Project site.
* For Solaris 64 bit, download the Apache web server from the Sunfreeware for Solaris Website.
* For Linux, the Apache web server is preinstalled on a Linux system.

Apache can communicate with JBoss using HTTP or the AJP protocol.

1. Uncomment the following module configurations in the *APACHE_HOME/conf/httpd.conf *file.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >For Linux, the default APACHE_HOME directory is /etc/httpd/.

1. Configure the proxy on port 8080 of JBoss.  
   Add the following configuration to the *APACHE_HOME/conf/httpd.conf* configuration file.

   ```java
   ProxyPass / http://<server_Name>:8080/
   ProxyPassReverse / http://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >When you use a proxy, the following configuration changes are required:
   >
   >    
   >    
   >    * Access: *http://&lt;server&gt;:&lt;port&gt;/system/console/configMgr*
   >    * Edit the configuration for Apache Sling Referrer Filter
   >    * In the Allow Hosts, add the entry for the proxy server
   >    
   >

1. Enable Compression.

   Add the following configuration to the *APACHE_HOME/conf/httpd.conf* configuration file.

   ```java
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
      
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

   4) To access the AEM server, use http://[Apache_server]:80.

[**Contact Support**](https://www.adobe.com/account/sign-in.supportportal.html)

<!--
<related-links>
<a href="../../forms/using/introduction-widgets.md">Appearance framework for adaptive and HTML5 forms</a>
<a href="../../forms/using/custom-profile.md">Creating custom profiles for HTML5 forms</a>
<a href="../../forms/using/custom-widgets.md">Custom Widgets for HTML5 forms</a>
<a href="../../forms/using/form-bridge-apis.md">Form Bridge for HTML5 forms</a>
<a href="../../forms/using/integrate-form-bridge-forms-portal.md">Integrating form bridge with forms portal</a>
<a href="../../forms/using/css-styles.md">Changing default styles of HTML5 forms</a>
</related-links>
-->
