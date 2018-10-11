---
title: Oak Queries and Indexing
seo-title: Oak Queries and Indexing
description: null
seo-description: Learn how to configure indexes in AEM.
uuid: 97c7d9f7-644e-4b29-8d1f-feaeef2bc90e
content-encoding: ISO-8859-1
aemsrcnodepath: /content/help/en/experience-manager/6-4/sites/deploying/using/queries-and-indexing
contentOwner: User
cq-designpath: /etc/designs/help
cq-lastmodified: 2018-04-30T03 27 30.658-0400
cq-lastmodifiedby: raiman
cq-lastreplicated: 2018-04-03T08 42 45.128-0400
cq-lastreplicatedby: carlino
cq-lastreplicationaction: Activate
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: deploying
cq-template: /apps/help/templates/article-3
discoiquuid: 516f58a5-af0b-4059-a045-aa981d52b455
firstPublishExternalDate: 2017-10-31T16:17:46.389-0400
isreadyforlocalization: false
jcr-created: 2018-02-22T08 02 59.329-0500
jcr-createdby: admin
jcr-ischeckedout: true
jcr-language: en_us
lastPublishExternalDate: 2018-04-03T08:42:44.180-0400
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
lochandoffdate: 2018-04-30T03 27 30.657-0400
lr-lastreplicatedby: carlino@adobe.com
moreHelpPaths: /content/help/en/experience-manager/6-4/sites/deploying/morehelp/deploying;/content/help/en/experience-manager/6-4/sites/deploying/morehelp/deploying
mwpw-migration-script-version: 2017-10-12T21 46 58.665-0400
navTitle: Oak Queries and Indexing
publishexternaldate: 2018-04-03T08 42 44.180-0400
publishExternalURL: https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/queries-and-indexing.html
qaDate: 2017-10-12T21:46:00.000-0400
qaNotes: /content/docs/en/aem/6-3/deploy/platform/queries-and-indexing
sha1: 91a8b213dd530361536afb1c33c9af37fedb58e1
topicBrowsingSortDate: 2018-04-03T08:42:44.180-0400
index: y
internal: n
snippet: y
translate: y
---

# Oak Queries and Indexing

>[!NOTE]
>
>This article is about configuring indexes in AEM 6. For best practices on optimizing query and indexing performance, see [Best Practices for Queries and Indexing](best-practices-for-queries-and-indexing.md).

## Introduction
Unlike Jackrabbit 2, Oak does not index content by default. Custom indexes need to be created when necessary, much like with traditional relational databases. If there is no index for a specific query, possibly many nodes will be traversed. The query may still work but probably be very slow.

If Oak encounters a query without an index, a WARN level log message is printed:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Supported query languages
The Oak query engine supports the following languages:

* XPath (recommended)
* SQL-2
* SQL (deprecated)
* JQOM

## Indexer types and cost calculation
The Apache Oak based backend allows different indexers to be plugged into the repository.

One indexer is the **Property Index**, for which the index definition is stored in the repository itself.

Implementations for **Apache Lucene** and **Solr **are also available by default, which both support fulltext indexing.

The **Traversal Index** is used if no other indexer is available. This means that the content is not indexed and content nodes are traversed to find matches to the query.

If multiple indexers are available for a query, each available indexer estimates the cost of executing the query. Oak then chooses the indexer with the lowest estimated cost.

![](assets/queries-and-indexing/chlimage_1.png)

The above diagram is a high level representation of the query execution mechanism of Apache Oak.

First, the query is parsed into an Abstract Syntax Tree. Then, the query is checked and transformed into SQL-2 which is the native language for Oak queries.

Next, each index is consulted to estimate the cost for the query. Once that is completed, the results from the cheapest index are retrieved. Finally, the results are filtered, both to ensure that the current user has read access to the result and that the result matches the complete query.

## Configuring the indexes

>[!NOTE]
>

Note: For a large repository, building an index is a time consuming operation. This is true for both the initial creation of an index, and reindexing (rebuilding an index after changing the definition). See also "Troubleshooting Oak Indexes" section "Preventing slow re-indexing".

If reindexing is needed in very large repositories, specially when using MongoDB and for fulltext indexes, consider text pre-extraction, and using oak-run to build the initial index and to reindex.

Indexes are configured as nodes in the repository under the **oak:index** node.

The type of the index node must be **oak:QueryIndexDefinition.** Several configuration options are available for each indexer as node properties. For more information, see the configuration details for each indexer type below.

### The Property Index
The Property Index is generally useful for queries that have property constraints but are not full-text. It can be configured by following the below procedure:

1. Open CRXDE by going to `http://localhost:4502/crx/de/index.jsp`
1. Create a new node under **oak:index**
1. Name the node **PropertyIndex**, and set the node type to **oak:QueryIndexDefinition**
1. Set the following properties for the new node:

    * **type: ** `property` (of type String)  
    
    * **propertyNames: ** `jcr:uuid` (of type Name)

   This particular example will index the `jcr:uuid` property, whose job is to expose the universally unique idetifier (UUID) of the node it is attached to.

1. Save the changes.

The Property Index has the following configuration options:

* The **type** property** **will specify the type of index, and in this case it must be set to **property**

* The **propertyNames** property indicates the list of the properties that will be stored in the index. In case it is missing, the node name will be used as a property name reference value. In this example, the **jcr:uuid** property whose job is to expose the unique identifier (UUID) of its node is added to the index.

* The** unique** flag which, if set to **true **adds a uniqueness constraint on the property index.  

* The **declaringNodeTypes** propery allows you to specify a certain node type that the index will only apply to.
* The **reindex** flag which if set to **true**, will trigger a full content reindex.

### The Ordered Index
The Ordered index is an extension of the Property index. However, it has been deprecated. Indexes of this type need to be replaced with the Lucene Property index (see below).

### The Lucene Full Text Index
A full text indexer based on Apache Lucene is available in AEM 6.

If a full-text index is configured, then all queries that have a full-text condition use the full-text index, no matter if there are other conditions that are indexed, and no matter if there is a path restriction.

If no full-text index is configured, then queries with full-text conditions will not work as expected.

Because the index is updated via an asynchronbous background thread, some full-text searches will be unavailable for a small window of time until the background processes are finished.

You can configure a Lucene full-text index, by following the below procedure:

1. Open CRXDE and create a new node under **oak:index**.
1. Name the node **LuceneIndex** and set the node type to **oak:QueryIndexDefinition**
1. Add the following properties to the node:

    * **type: ** `lucene` (of type String)  
    
    * **async: ** `async` (of type String)

1. Save the changes.

The Lucene Index has the following configuration options:

* The **type** property which will specify the type of index must be set to **lucene**

* The **async** property which must be set to **async**. This will send the index update process to a background thread.

* The **includePropertyTypes** property, which will define what subset of property types will be included in the index.
* The **excludePropertyNames** property which will define a blacklist of property names - properties that should be excluded from the index.
* The **reindex** flag which when set to **true**, triggers a full content re-index.

### The Lucene Property Index
Since **Oak 1.0.8**, Lucene can be used to create indexes which involve property constraints that are not full-text.

In order to achieve a Lucene Property Index the **fulltextEnabled** property must always be set to false.

Take the following example query:

```xml
select * from [nt:base] where [alias] = '/admin'
```

In order to define a Lucene Property Index for the above query, you can add the following definition by creating a new node under **oak:index:**

* **Name:** `LucenePropertyIndex`

* **Type:** `oak:QueryIndexDefinition`

Once the node has been created, add the following properties:

* **type:** `lucene (of type String)  
  `

* **async:** `async (of type String)  
  `

* **fulltextEnabled:** `false (of type Boolean)  
  `

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>Compared to the regular Property Index, the Lucene Property Index is always configured in async mode. Thus, the results returned by index may not always reflect the most up to date state of the repository.

>[!NOTE]
>
>For more specific information on the Lucene Property Index, see the [Apache Jackrabbit Oak Lucene documentation page](http://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene Analyzers
Since version 1.2.0, Oak supports Lucene analyzers.

Analyzers are used both when a document is indexed, and at query time. An analyzer examines the text of fields and generates a token stream. Lucene analyzers are composed of a series of tokenizer and filter classes.

The analyzers can be configured via the `analyzers` node (of type `nt:unstructured`) inside the `oak:index` definition.

The default analyzer for an index is configured in the `default` child of the analyzers node.

![](assets/queries-and-indexing/chlimage_1-1.png)

>[!NOTE]
>
>For a list of available analyzers, please consult the API documentation of the Lucene version you are using.

#### Specifying the Analyzer Class Directly
If you wish to use any out of the box analyzer, you can configure it following the below procedure:

1. Locate the index you wish to use the analyzer with under the `oak:index` node.  

1. Under the index, create a child node called `default` of type `nt:unstructured`.  

1. Add a property to the default node with the following properties:

    * **Name:** `class`
    
    * **Type:** `String`
    
    * **Value:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   The value is the name of the analyzer class you wish to use.

   You can also set the analyzer to be used with a specific lucene version by using the optional `luceneMatchVersion` string propery. A valid synthax for using it with Lucene 4.7 would be:

    * **Name:** `luceneMatchVersion`
    
    * **Type:** `String`
    
    * **Value:** `LUCENE_47`

   If `luceneMatchVersion` is not provided, Oak will use the version of Lucene it is shipped with.

1. If you wish to add a stopwords file to the analyzer configurations, you can create a new node under the `default` one with the following properties:

    * **Name:** `stopwords`
    
    * **Type:** `nt:file`

#### Creating Analyzers via Composition
Analyzers can also be composed based on `Tokenizers`, `TokenFilters` and `CharFilters`. You can do this by specifying an analyzer and creating children nodes of its optional tokenizers and filters which will be applied in listed order. [](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Consider this node structure as an example:

* **Name:** `analyzers`

    * **Name:** `default`

        * **Name:** `charFilters`
        
        * **Type:** `nt:unstructured`

            * **Name:** `HTMLStrip`
            
            * **Name:** `Mapping`

        * **Name:** `tokenizer`

            * **Property Name:** `name`

                * **Type:** `String`
                
                * **Value:** `Standard`

        * **Name:** `filters`
        
        * **Type:** `nt:unstructured`

            * **Name:** `LowerCase`
            
            * **Name:** `Stop`

                * **Property name:** `words`

                    * **Type:** `String`
                    
                    * **Value:** `stop1.txt, stop2.txt`

                * **Name:** `stop1.txt`

                    * **Type:** `nt:file`

                * **Name:** `stop2.txt`

                    * **Type:** `nt:file`

The name of the filters, charFilters and tokenizers are formed by removing the factory suffixes. Thus:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` becomes `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` becomes `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` becomes `Stop`

Any configuration parameter required for the factory is specified as property of the the node in question.

For cases such as loading stop words where content from external files needs to be loaded, the content can be provided by creating a child node of `nt:file` type for the file in question.

### The Solr Index
The purpose of the Solr index is mainly full-text search but it can also be used to index search by path, property restrictions and primary type restrictions. This means the Solr index in Oak can be used for any type of JCR query.

The integration in AEM happens at the repository level so that Solr is one of the possible indexes that can be used in Oak, the new repository implementation shipped with AEM.

It can be configured to work as an embedded server with the AEM instance, or as a remote server.

### Configuring AEM with an embedded Solr server

>[!CAUTION]
>
>Do not use an embedded Solr server in a production enviroment. It should be used only in a development enviroment.

AEM can be used with an embedded Solr server that can be configured via the Web Console. In this case, the Solr server will run in the same JVM as the AEM instance it is embedded to.

You can configure the embedded Solr server by:

1. Going to the Web Console at `http://serveraddress:4502/system/console/configMgr`
1. Search for "**Oak Solr server provider**".
1. Press the edit button and in the following window set the server type to **Embedded Solr** in the drop-down list.  

1. Next, edit "**Oak Solr embedded server configuration**" and create a configuration. For more info on the configuration options, please visit the [Apache Solr website](http://lucene.apache.org/solr/documentation.html).

   >[!NOTE]
   >
   >The Solr home directory (solr.home.path) configuration will look for a folder with the same name in the AEM installation folder.

1. Open CRXDE and login as Admin.
1. Add a node called **solrlndex** of type **oak:QueryIndexDefinition **under **oak:index** with the following properties:

    * **type:** `solr`(of type String)
    
    * **async:** `async`(of type String)
    
    * **reindex:** `true`(of type Boolean)

1. Save the changes.

### Configuring AEM with a single remote Solr server
AEM can also be confiured to work with a remote Solr server instance:

1. Download and extract the latest version of Solr. For more info on how to do this, please consult the [Apache Solr Installation documentation](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. Now, create two Solr shards. You can do this by creating folders for each shard in the folder where Solr has been upacked:

    * For the first shard, create the folder: ``

   `<solrunpackdirectory>\aemsolr1\node1`

    * For the second shard, create the folder: ``

   `<solrunpackdirectory>\aemsolr2\node2`

1. Locate the example instance in the Solr package. It is usually located in a folder called " `example`" in the root of the package.
1. Copy the following folders from the example instance to the two shard folders ( `aemsolr1\node1` and `aemsolr2\node2`):

    * `contexts`
    * `etc`
    * `lib`
    * `resources`
    * `scripts`
    * `solr-webapp`
    * `webapps`
    * `start.jar`

1. Create a new folder called " `cfg`" in each of the two shard folders.
1. Place your Solr and Zookeeper configuration files in the newly created `cfg` folders.

   >[!NOTE]
   >
   >For more info on Solr and ZooKeeper configuration, consult the [Solr Configuration documentation](https://wiki.apache.org/solr/ConfiguringSolr) and the [ZooKeeper Getting Started Guide](http://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Start the first shard with ZooKeeper support by going to `aemsolr1\node1` and running the following command:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Start the second shard by going to `aemsolr2\node2` and running the following command:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. After both shards have been started, test that everything is up and running by connecting to the Solr interface at `http://localhost:8983/solr/#/`
1. Start AEM and go to the Web Console at `http://localhost:4502/system/console/configMgr`
1. Set the following configuration under **Oak Solr remote server configuration**:

    * Solr HTTP URL: `http://localhost:8983/solr/`

1. Choose **Remote Solr** in the drop down list under **Oak Solr** server provider.  

1. Go to CRXDE and login as Admin.
1. Create a new node called **solrIndex** under **oak:index**, and set the following properties:

    * **type:**solr (of type String)
    * **async:**async (of type String)
    * **reindex:**true (of type Boolean)

1. Save the changes.

#### Recommended configuration for Solr
Below is an example of a base configuration that can be used with all three Solr deployments described in this article. It accomodates the dedicated property indexes that are already present in AEM and should not be used with other applications.

In order to properly use it, you need to place the contents of the archive directly in the Solr Home Directory. In the case of multi-node deployments, it should go directly under the root folder of each node.

<!-- 

Comment Type: remark
Last Modified By: unknown unknown (ims-author-AAC0465A528DC04F0A490D44@AdobeID)
Last Modified Date: 2018-02-22T05:06:45.702-0500

<p>The ACS Indexing tools are a part of the product since 6.1, and will be moved to the Ops Dashboard page. See DOC-5152 and DOC-5138</p>

 -->

### AEM Indexing Tools
AEM 6.1 also integrates two indexing tools present in AEM 6.0 as part of the Adobe Consulting Services Commons toolset:

1. **Explain Query**, a tool designed to help administrators understand how queries are executed;
1. **Oak Index Manager**, a Web User Interface for maintaining existing indexes.

You can now reach them by going to **Tools - Operations - Dashboard - Diagnosis** from the AEM Welcome screen.

For more information on how to use them, see the [Operations Dashboard documentation](/content/help/en/experience-manager/6-4/sites/administering/using/operations-dashboard).

### ACS Commons Indexing Tools
The [Adobe Consulting Service Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) toolkit introduces a set of indexing tools in an effort to simplify management and maintenance of indexes in the underlining data storage layer of AEM, Apache OAK.

The tools are:

* **Explain Query**, a tool designed to help administrators understand how queries are executed;  

* **Oak Index Manager**, a Web User Interface for maintaining existing indexes.

>[!NOTE]
>
>Starting with AEM 6.1, both the Explain Query and Oak Index Manager tools will ship with product, thus eliminating the need to install the separately.
>
>You can reach them by going to **Tools - Operations - Dashboard - Diagnosis** from the AEM Welcome screen.

#### The Explain Query Tool
For any given query, Oak attempts to figure out the best way to execute based on the Oak indexes defined in the repository under the **oak:index** node. Depending on the query, different indexes may be chosen by Oak. Understanding how Oak is executing a query is the first step to optimizing the query.

The Explain Query is a tool that explains how Oak is executing a query.

**Features**

* Supports the Xpath, JCR-SQL and JCR-SQL2 query languages  
* Reports the actual execution time of the provided query  
* Detects slow queries and warns about queries that could be potentially slow**** 

* Reports the Oak index used to execute the query
* Displays the actual Oak Query engine explanation
* Provides click-to-load list of Slow and Popular queries

**Installing Explain Query**

Explain Query is part of the ACS Toolset and can be installed as a standard AEM package. In order to use it, you need to:

1. Go to the [ACS Tools Website](https://adobe-consulting-services.github.io/acs-aem-tools/) and download the package.
1. Go to `http://localhost:4502/crx/packmgr/index.js`p to access the Package Manager.
1. Upload the package and install it. For more information on how to work with Package Manager, see [How to Work with Packages](/content/help/en/experience-manager/6-4/sites/administering/using/package-manager#main-pars_title_10).
1. Access the Explain Query UI by pointing your browser to `http://localhost:4502/etc/acs-tools/explain-query.html`

Once in the Explain Query UI, select the query language, enter a query and press the Explain button.

![](assets/queries-and-indexing/chlimage_1-2.png)

The first entry in the Query Explanation section is the actual explanation. The explanation will show the type of index that was used to execute the query.

The second entry is the query plan.

Ticking the **Include exectuion time** box before running the query will also show the amount of time the query was executed in, allowing for more information that can be used for optimizing the indexes for your application or deployment.

The tool will also build a list of popular and slow queries that can be automatically loaded in the UI by clicking their name in the predefined list, as shown below.

![](assets/queries-and-indexing/chlimage_1-3.png) 

#### The Oak Index Manager
The Oak Index Manager is a simple WebUI created to facilitate index management such as maintaining indexes, viewing their status or triggering re-indexes.

It can be downloaded as a part of the [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) package and installed via Package Manager in AEM.

Once installed, it can be accessed by going to **Tools - ACS AEM Commons - Oak Index Manager** from the welcome screen or by directly accesing the url at `http://localhost:4502/etc/acs-commons/oak-index-manager.html`

![](assets/queries-and-indexing/chlimage_1-4.png)

The UI can be used to filter indexes in the table by typing in the filter criteria in the search box in the upper left corner of the screen.

A single reindex can be triggered by clicking the icon in the **Reindex** column for the respective index. A bulk reindex can be triggered by selecting multiple indexes and clicking the **Bulk Reindex** button.

#### Creating Property Indexes via OSGi
The ACS Commons package also exposes OSGi configurations that can be used to create property indexes.

You can access it from the Web Console by searching for "**Ensure Oak Property Index**".

![](assets/queries-and-indexing/chlimage_1-5.png) 

### Troubleshooting indexing issues
Situations may arise where queries take a long time to execute, and the general system response time is slow.

This section presents a set of recommendations on what needs to be done in order to track down the cause of such issues and advice on how to resolve them.

#### Preparing Debugging Info for Analysis
The easiest way to get required information for the query being executed is via the [Explain Query tool](/content/help/en/experience-manager/6-4/sites/administering/using/operations-dashboard#main-pars_title_1097830066). This will enable you to collect the precise information that is needed to debug a slow query without the need to consult the log level information. This is desirable if you know the query that is being debugged.

If this is not possible for any reason, you can gather the indexing logs in a single file and use it to troubleshoot your particular problem.

#### Enable Logging
To enable logging, you need to enable **DEBUG** level logs for the categories pertaining to Oak indexing and queries. These categories are:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

The **com.day.cq.search** category is only applicable if you are using the AEM provided QueryBuilder utility.

>[!NOTE]
>
>It is important that the logs are only set to DEBUG for the duration the query you want to troubleshoot is being executed, otherwise a large amount of events will be generated in the logs over time. Because of this, once the required logs are collected switch back to INFO level logging for the categories mentioned above.

You can enable logging by following this procedure:

1. Point your browser to `http://serveraddress:port/system/console/slinglog`
1. Click the **Add new Logger** button in the lower part of the console.  

1. In the newly created row, add the categories mentioned above. You can use the **+** sign to add more than one category to a single logger.  

1. Choose **DEBUG** from the **Log level** drop down list.  

1. Set the output file to `logs/queryDebug.log`. This will correlate all the DEBUG events into a single log file.  

1. Run the query or render the page that is using the query you wish to debug.  

1. Once you have executed the query, go back to the logging console and change the log level of the newly created logger to **INFO**.

#### Index Configuration
The way the query gets evaluated is largely affected by the index configuration. It is important to get the index configuration in order to be analyzed or sent to support. You can either get the configuration as a content package or get a JSON rendition.

Since in most cases, the indexing configuration is stored under the `/oak:index` node in CRXDE, you can get the JSON version at:

`http://serveraddress:port/oak:index.tidy.-1.json`

If the index is configured at a different location, change the path accordingly.

#### MBean output
In some cases it is helpful to provide the output of index related MBeans for debugging. You can do this by:

1. Going to the JMX console at: http://serveraddress:port/system/console/jmx  

1. Search for the following MBeans:

    * Lucene Index statistics
    * CopyOnRead support statistics
    * Oak Query Statistics
    * IndexStats

1. Click each of the MBeans to get the performance statistics. Create a screenshot or note them down in case submission to support is required.

You can also get the JSON variant of these statistics at the following URLs:

* `http://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `http://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `http://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `http://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

You can also provide consolidated JMX output via `http://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. This would include all Oak related MBean details in JSON format.

#### Other Details
You can gather additional details in order to help troubleshoot the problem, such as:

1. The Oak version your instance is running on. You can see this by opening CRXDE and looking at the version in the lower right corner of the welcome page, or by checking the version of the `org.apache.jackrabbit.oak-core` bundle.
1. The QueryBuilder Debugger output of the troublesome query. The debugger can be accessed at: `http://serveraddress:port/libs/cq/search/content/querydebug.html`
