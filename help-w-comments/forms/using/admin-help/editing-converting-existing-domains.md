---
title: Editing and converting existing domains
seo-title: Editing and converting existing domains
description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa. 
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa. 
uuid: 717dad7f-7838-4b8b-9c06-9a5b470cf631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 40ed761d-0dae-4cd9-aa9d-e4d6ddffd6ea
index: y
internal: n
snippet: y
---

# Editing and converting existing domains{#editing-and-converting-existing-domains}

You can change the settings for existing domains from the Domain Management page. You can also convert an existing enterprise domain to a hybrid domain.

## Edit an existing domain {#edit-an-existing-domain}

1. In administration console, click Settings &gt; User Management &gt; Domain Management.
1. Click the name of the domain to edit. 
1. To change the domain name, change the text in the Name box. 
1. To change the authentication information for an enterprise or hybrid domain, click the appropriate authentication name at the bottom of the page. On the Edit Authentication page, change settings as required. (See [Authentication settings](../../../forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. To change the directory information for an enterprise domain, click the appropriate directory name at the bottom of the page. On the Edit Directory page, change settings as required. (See [Adding directories or custom SPIs](../../../forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. When you complete your changes, click OK.

## Convert an enterprise domain to a hybrid domain {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. In administration console, click Settings &gt; User Management &gt; Domain Management.
1. Click the name of the enterprise domain to convert. 
1. Click Convert to Hybrid Domain.
1. Review the information that appears regarding user and group data and authentication of users, and click OK.
1. Edit the settings for the hybrid domain and click OK.

>[!NOTE]
>
>If the enterprise domain that you are converting does not contain directory settings, any LDAP authentication settings are lost.

## Convert a hybrid domain to an enterprise domain {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. In administration console, click Settings &gt; User Management &gt; Domain Management.
1. Click the name of the hybrid domain to convert. 
1. Click Convert to Enterprise Domain.
1. Review the information that appears regarding user and group data and authentication of users, and click OK.
1. Click Add Directory and configure the required directory information. (See [Adding directories or custom SPIs](../../../forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
