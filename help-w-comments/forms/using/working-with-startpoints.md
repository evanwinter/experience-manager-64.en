---
title: Working with Startpoints
seo-title: Working with Startpoints
description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 95cc8ca4-d9a6-4b04-905e-af4ac3b10a84
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: faacb44e-7d55-4bb4-8e72-0c2fa51e1924
index: y
internal: n
snippet: y
---

# Working with Startpoints{#working-with-startpoints}

A startpoint invokes a process created in Workbench. It is associated with a form which invokes the process when the form is submitted. See [Geometrixx Finance Reference Site walkthrough](../../forms/using/finance-reference-site-walkthrough.md) to understand processes.

>[!NOTE]
>
>The terms startpoints, start process, and form are used interchangably when referrring to this concept.

To initiate a process from the AEM Forms app, you need to have a startpoint of type **Workspace **in your process. Also, you need to select the **[!UICONTROL Visibile in Mobile Workspace]** option for the startpoint.

![](assets/mws_startpoint_select_option.png)

**To start a process defined in Workbench**

1. To view the Startpoints available in the AEM Forms app, go to [Home screen](../../forms/using/home-screen.md).
1. On the **[!UICONTROL Home]**screen, by default, the **[!UICONTROL All Forms]**list is displayed.

   The startpoint is associated with a form. Tap the startpoint associated form in the list to open it.

   The form associated with the startpoint opens.

1. Enter the details in the **[!UICONTROL Startpoint]**form.

   <!--
   Comment Type: draft

   <p>You can <a href="/forms/using/save-as-draft1.md" target="_blank">save a draft</a> of the updates to this Startpoint and complete this at a later time.</p>
   -->

   You can add annotations to this task using the [attachment](../../forms/using/add-attachments.md) button.

1. After you fill the form, tap the **Submit** button.

If the app is offline, the form and its data is saved in the Outbox folder.

If the app is online, the task is synchronized with the AEM Forms server and assigned to the user specified in the process.

To work with the task in your task list, see [Opening a task](../../forms/using/open-task.md).

[**Contact Support**](https://www.adobe.com/account/sign-in.supportportal.html)

<!--
<related-links>
<a href="../../forms/using/open-task.md">Opening a task</a>
<a href="../../forms/using/working-with-form.md">Working with a Form</a>
<a href="../../forms/using/add-attachments.md">Adding attachments</a>
<a href="../../forms/using/save-as-draft.md">Saving a task (Save as Draft)</a>
</related-links>
-->
