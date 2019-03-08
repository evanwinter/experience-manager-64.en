---
title: Enhanced sorting of assets in AEM
seo-title: Enhanced Sort
description: Learn how AEM Assets deploys server-side sorting to sort folder assets or a search query at one go instead of sorting them in batches on the client side.
seo-description: Learn how AEM Assets deploys server-side sorting to sort folder assets or a search query at one go instead of sorting them in batches on the client side.
uuid: 9bd02d23-8d35-4f1f-a51c-cb29248f0aa7
contentOwner: asgupta
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 73b17c0f-732d-4255-8700-054717992304
index: y
internal: n
snippet: y
---

# Enhanced sorting of assets in AEM{#enhanced-sorting-of-assets-in-aem}

Learn how AEM Assets deploys server-side sorting to sort folder assets or a search query at one go instead of sorting them in batches on the client side.

The search capability of Adobe Experience Manager (AEM) Assets is enhanced to efficiently sort a large number of assets in the folder list view and search results pages. You can also sort timeline entries.

AEM Assets deploys server-side sorting to sort the entire set of assets (howsoever large) within a folder or a search query at one go instead of sorting them in batches on the client side. This way, prefetched results can be quickly displayed on the user interface, which makes the sort operation more responsive and brisk.

## Sorting assets in List view {#sorting-assets-in-list-view}

AEM Assets lets you sort folder assets based on the following fields:

* Locale
* Status
* Type
* Size
* Rating
* Date modified
* Date published
* Usage
* Clicks
* Impressions
* Checked out

1. Navigate to a folder that contains a large a number of assets.
1. Click/tap the Layout icon and toggle to the list view.

   ![](assets/chlimage_1-402.png)

1. Click/tap the Sort icon beside any column header in the list of assets.

   ![](assets/chlimage_1-403.png)

   The list of assets is sorted based on the field values.

   ![](assets/chlimage_1-404.png)

>[!NOTE]
>
>To sort the values in the `Name` or the `Title`columns, overlay `/libs/dam/gui/content/commons/availablecolumns` and change the value of `sortable` to `True`.

## Sorting assets in search results {#sorting-assets-in-search-results}

You can sort search results based on the following fields:

* Title
* Status
* Type
* Size
* Date modified
* Date published

1. From the OmniSearch box, search for assets based on the desired criteria.

   ![](assets/chlimage_1-405.png)

1. Click/tap the Layout icon and toggle to the list view. If the search results are already displayed in the list view, skip this step.
1. Click/tap the Sort icon beside any column header in the list of assets. The list of assets is sorted based on the field values.

   ![](assets/chlimage_1-406.png)

## Sorting assets in timeline {#sorting-assets-in-timeline}

AEM Assets lets you chronologically sort timeline entries, such as annotations, versions, workflows, and activities.

1. From the Assets UI, select an asset for which you want to display the timeline.
1. Click/tap the GolbalNav icon and select **Timeline**.

   ![](assets/chlimage_1-407.png)

1. In the timeline, select an entry from the list. For example, select **Comments** to display the list of annotations associated with the asset. 

   ![](assets/chlimage_1-408.png)

1. Click/tap the **Sort** icon beside the **Date** label. Based on your selection, the annotations are listed in the chronological/reverse chronological order in which they were added to the asset.

   ![](assets/chlimage_1-409.png)
