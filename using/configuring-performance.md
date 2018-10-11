---
title: Performance Optimization
seo-title: Performance Optimization
description: null
seo-description: Learn how to configure certain aspects of AEM to optimize performance.
uuid: 77ffbafe-7a80-46bd-9318-bca622c96fe5
content-encoding: ISO-8859-1
aemsrcnodepath: /content/help/en/experience-manager/6-4/sites/deploying/using/configuring-performance
contentOwner: User
cq-designpath: /etc/designs/help
cq-lastmodified: 2018-04-30T03 27 44.461-0400
cq-lastmodifiedby: carlino
cq-lastreplicated: 2018-04-03T08 40 06.708-0400
cq-lastreplicatedby: carlino
cq-lastreplicationaction: Activate
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: configuring
cq-template: /apps/help/templates/article-3
discoiquuid: 4475d1f8-7f84-4b9c-96de-b10349160deb
firstPublishExternalDate: 2017-10-31T16:18:10.201-0400
isreadyforlocalization: false
jcr-created: 2017-12-01T19 03 38.005-0500
jcr-createdby: admin
jcr-ischeckedout: true
jcr-language: en_us
jcr-lastmodifiedby: remove-legacypath-6-1
lastPublishExternalDate: 2018-04-03T08:40:05.815-0400
lochandoffdate: 2018-04-30T03 27 44.460-0400
lr-lastreplicatedby: carlino@adobe.com
moreHelpPaths: /content/help/en/experience-manager/6-4/sites/deploying/morehelp/configuring;/content/help/en/experience-manager/6-4/sites/deploying/morehelp/configuring
mwpw-migration-script-version: 2017-10-12T21 46 58.665-0400
navTitle: Performance Optimization
publishexternaldate: 2018-04-03T08 40 05.815-0400
publishExternalURL: https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/configuring-performance.html
qaDate: 2017-10-12T21:46:00.000-0400
qaNotes: /content/docs/en/aem/6-3/deploy/configuring/performance
sha1: c9eca41f7778247646ec27c9b46ec88892cc86e2
topicBrowsingSortDate: 2018-04-03T08:40:05.815-0400
index: y
internal: n
snippet: y
translate: y
---

# Performance Optimization

>[!NOTE]
>
>For general guidelines about performance, read the [Performance Guidelines](performance-guidelines.md) page.
>
>For more information about troubleshooting and fixing performance issues, also see the [Performance tree](performance-tree.md).
>
>Additionallty, you can review a Knowlege Base article on [Performance Tuning Tips.](/content/help/en/experience-manager/kb/performance-tuning-tips)

A key issue is the time your website takes to respond to visitor requests. Although this value will vary for each request, an average target value can be defined. Once this value is proven to be both achievable and maintainable, it can be used to monitor the performance of the website and indicate the development of potential problems.

The response times you will be aiming for will be different on the author and publish environments, reflecting the different characteristics of the target audience:

#### Author Environment
This environment is used by authors entering, and updating content. It must cater for a small number of users who each generate a high number of performance intensive requests when updating content pages and the individual elements on those pages.

#### Publish Environment
This environment contains content which you make available to your users. Here the number of requests is even greater and the speed is just as vital, but since the nature of the requests is less dynamic, additional performance enhancing mechanisms can be applied; such as caching the content or load-balancing.

>[!NOTE]
>
>* After configuring for performance optimization, follow the procedures in [Tough Day](/content/help/en/experience-manager/6-4/sites/developing/using/tough-day) to test the environment under heavy load.
>* See also [Performance tuning tips](/content/help/en/experience-manager/kb/performance-tuning-tips).
>

## Performance Optimization Methodology
A performance optimization methodology for CQ projects can be summed up in five very simple rules that can be followed to avoid performance issues from the start:

1. [Planning for Optimization](#PlanningforOptimization)
1. [Simulate Reality](#SimulateReality)
1. [Establish Solid Goals](#EstablishSolidGoals)
1. [Stay Relevant](#StayRelevant)
1. [Agile Iteration Cycles](#AgileIterationCycles)

These rules, to a large degree, apply to web projects in general, and are relevant to project managers and system administrators to ensure that their projects will not face performance challenges when launch time comes.

### Planning for Optimization
![](assets/configuring-performance/chlimage_1.jpeg)

Around 10% of the project effort should be planned for the performance optimization phase. Of course, the actual performance optimization requirements will depend on the level of complexity of a project and the experience of the development team. While your project may (ultimately) not require all of the allocated time, it is good practice to always plan for performance optimization in the suggested region.

Whenever possible, a project should first be soft-launched to a limited audience in order to gather real-life experience and perform further optimizations, without the additional pressure that follows a full announcement.

Once you are "live", performance optimization is not over. This is the point in time when you experience the "real" load on your system. It is important to plan for additional adjustments after the launch.

Since your system load changes and the performance profiles of your system shifts over time, a performance "tune-up" or "health-check" should be scheduled at 6-12 months intervals.

### Simulate Reality
![](assets/configuring-performance/chlimage_1-1.jpeg)

If you go live with a website and find out after the launch that you run into performance issues there is only one reason for that: Your load and performance tests did not simulate reality closely enough.

Simulating reality is difficult and how much effort you will reasonably want to invest into getting "real" depends on the nature of your project. "Real" means not just "real code" and "real traffic", but also "real content", especially regarding content size and structure. Keep in mind that your templates may behave completely different depending on the size and structure of the repository.

### Establish Solid Goals
![](assets/configuring-performance/chlimage_1-2.jpeg)

The importance of properly establishing performance goals is not to be underestimated. Often, once people become focused on specific performance goals it is very hard to change these goals afterwards, even if they are based on wild assumptions.

Establishing good, solid performance goals is really one of the trickiest areas. It is often best to collect real life logs and benchmarks from a comparable website (for example the new website's predecessor).

### Stay Relevant
![](assets/configuring-performance/chlimage_1-3.jpeg)

It is important to optimize one bottleneck at a time. If you try to do things in parallel without validating the impact of the one optimization, you will lose track of which optimization measure actually helped.

### Agile Iteration Cycles
![](assets/configuring-performance/chlimage_1-4.jpeg)

Performance tuning is an iterative process that involves, measuring, analysis, optimization and validation until the goal is reached. In order to properly take this aspect into account, implement an agile validation process in the optimization phase rather than a more heavy-weight testing process after each iteration.

This largely means that the developer implementing the optimization should have a quick way to tell if the optimization has already reached the goal. This is valuable information, because when the goal is reached, optimization is over.

## Basic Performance Guidelines
Generally speaking, keep your uncached html requests to less than 100ms. More specifically, the following may serve as a guideline:

* 70% of the requests for pages should be responded to in less than 100ms.
* 25% of the requests for pages should get a response within 100ms-300ms.
* 4% of the requests for pages should get a response within 300ms-500ms.
* 1% of the requests for pages should get a response within 500ms-1000ms.
* No pages should respond slower than 1 second.

The above numbers assume the following conditions:

* measured on publish (no overheads as related to an authoring environment)
* measured on the server (no network overhead)
* not cached (no CQ-output cache, no Dispatcher cache)
* only for complex items with many dependencies (HTML, JS, PDF, ...)
* no other load on the system

There are a certain number of issues that frequently contribute to performance problems. These mainly revolve around:

* dispatcher caching inefficiency
* the use of queries in normal display templates.

JVM and OS level tuning do not usually lead to big leaps in performance and should therefore be performed at the very end of the optimization cycle.

The way a content repository is structured can impact performance as well. For best performance, the number of child nodes attached to individual nodes in a content repository should not exceed 1,000 (as a general rule).

Your best friends during a usual performance optimization exercise are:

* the `request.log`
* component based timing
* last but not least a java profiler.

### Performance when loading and editing Digital Assets
Due to the large volume of data involved when loading and editing digital assets, performance can become an issue.

Two things affect performance here:

* CPU - multipe cores allow for smoother work when transcoding
* Hard disk - parallel RAID disks achieve the same

To improve performance you can consider the following:

* How many assets are going to be uploaded per day? A good estimate can be based on:

![](assets/configuring-performance/chlimage_1.png)

* The timeframe in which edits will be made (typically the length of the working day, more for international operations).
* The average size of images uploaded (and the size of renditions generated per image) in megabytes.
* Determine the average data rate:

![](assets/configuring-performance/chlimage_1-1.png)

* 80% of all edits will be made in 20% of the time, so in peak time you will have 4 times the average data rate. This is your performance goal.

## Performance Monitoring
Performance (or the lack of it) is one of the first things that your users notice, so as with any application with a user interface, performance is of key importance. To optimize the performance of your CQ installation you need to monitor various attributes of the instance and its behavior.

For information about how to perform performance monitoriing, see [Monitoring Performance](monitoring-and-maintaining.md#main-pars_title_3).

The problems that cause performance issues are often difficult to track down, even when their effects are easy to see.

A basic starting point is a good knowledge of your system when it is operating as normal. Unless you know how your environment "looks" and "behaves" when it is performing properly, it can be difficult to locate the problem when performance deteriorates. This means that you should spend some time investigating your system when it is running smoothly and ensure that collecting performance information is an ongoing task. This will provide you with a basis for comparison should the performance suffer.

The following diagram illustrates the path that a request for CQ content can take - and therefore the number of different elements which can impact the performance.

![](assets/configuring-performance/chlimage_1-2.png)

Performance is also a balance between Volume and Capacity:

This can be illustrated in various locations throughout the web-chain.

![](assets/configuring-performance/chlimage_1-3.png)

There are several functional areas which are often responsible for impacting the performance:

* Caching
* Application (your project) code
* Search functionality

### Basic Rules Regarding Performance
Certain rules should be kept in mind when optimizing performance:

* Performance tuning *must* be part of every project.
* Do not optimize early in the development cycle.
* Performance is only as good as the weakest link.
* Always think about capacity vs. volume.
* Optimize important things first.
* Never optimize without *realistic* goals.

>[!NOTE]
>
>Bear in mind that the mechanism you use to measure performance will often affect exactly what you are trying to measure. You should always try to account for these discrepancies, and eliminate as much of their effect as possible; in particular browser plug-ins should be de-activated wherever possible.

## Configuring for Performance
Certain aspects of CQ (and/or the underlying CRX) can be configured to optimize performance. The following are possibilities and suggestions, you must sure of whether, or how, you use the functionality in question before making changes.

>[!NOTE]
>
>For additional information please see the [KB article](/content/help/en/experience-manager/kb/performance-tuning-tips).

<!-- 

Comment Type: remark
Last Modified By: Alison Heimoz (aheimoz)
Last Modified Date: 2017-11-30T05:41:46.145-0500

<p>"Disable Cluster Mode" - to be left as a KB-article only (see Greg).<br /> </p>

 -->

### Search Indexing
Starting in AEM 6.0, Adobe Experience Manager uses an Oak based repository architecture.

You can find the updated indexing information here:

* [Best Practices for Queries and Indexing](best-practices-for-queries-and-indexing.md)
* [Queries and Indexing](/queries-and-indexing.html )

### Concurrent Workflow Processing
Limit the number of concurrently running workflow processes to improve performance. By default, the workflow engine processes as many workflows in parallel as there are processors available to the Java VM. When workflow steps require large amounts of processing resources (RAM or CPU), running several of these workflows in parallel can place high demans on available server resources.

For example, when images (or DAM assets in general) are uploaded, workflows automatically import the images into DAM. Images are often high-resolution and that can easily consume hundreds of MB of heap for processing. Handling these images in parallel places a high load on the memory subsystem and the garbage collector.

The workflow engine uses Apache Sling job queues for handling and scheduling work item processing. The following job queue services have been created by default from the Apache Sling Job Queue Configuration service factory for processing workflow jobs:

* Granite Workflow Queue: Most workflow steps, such as the ones that process DAM assets, use the Granite Workflow Queue service.
* Granite Workflow External Process Job Queue: This service is used for special extermal workflow steps that are typically used for contacting an external system and polling for results. For example the InDesign Media Extraction Process step is implemented as an external process. The workflow engine uses the external queue for processing the polling. (See [com.day.cq.workflow.exec.WorkflowExternalProcess](/content/help/en/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess).)

Configure these services to limit the maximum number of concurrently running workflow processes.

**Note:** Configuring these job queues affects all workflows unless you have created a job queue for a specific workflow model (see [Configure the Queue for a Specific Workflow Model](configuring-performance.md#main-pars_title_13) below).

**Configuration in the Repository **

If you are configuring the services [using a sling:OsgiConfig node](configuring-osgi.md#main-pars_title_3), you need to find the PID of the existing services, for example: org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. You can discover the PID using the Web Console.

You need to configure the property named queue.maxparallel.

**Configuration in the Web Console**

To configure these services [using the Web Console](configuring-osgi.md#main-pars_title_104), locate the existing configuration items below the Apache Sling Job Queue Configuration service factory.

You need to configure the property named Maximum Parallel Jobs.

### Configure the Queue for a Specific Workflow
Create a job queue for a specific workflow model so that you can configure job handling for that workflow model. In this way, your configurations affect the processing for a specific workflow, while the configuration of the default Granite Workflow Queue controls the processing of other workflows.

When workflow models execute, they create Sling jobs for a specific topic. By default, the topic matches the topics that are configured for the general Granite Workflow Queue, or the Granite Workflow External Process Job Queue:

* com/adobe/granite/workflow/job&#42;
* com/adobe/granite/workflow/external/job&#42;

Actual job topics that worflow models generate include model-specific suffix. For example, the DAM Update Asset workflow model generates jobs with the following topic:

com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model

Therefore, you can create a job queue for the topic that matches the job topics of your workflow model. Configuring the performance-related properties of the queue affects only the worklfow model that generates the jobs that match the queue topic.

The following procedure creates a job queue for a workflow, using the DAM Update Asset workflow as an example.

1. Execute the workflow model for which you want to create the job queue, so that topic statistics are generated. For example, add an image to Assets to execute the DAM Update Asset workflow. 
1. Open the Sling Jobs console. ( [http://localhost:4502/system/console/slingevent](http://localhost:4502/system/console/slingevent))
1. Discover the workflow-related topics in the console. For DAM Update Asset, the following topics are found:

    * com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model
    * com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model
    * com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model

1. Create one job queue for each of these topics. To create a job queue, create a factory configuration for the Apache Sling Job Queue factory service.

   The factory configurations are similar to the Granite Workflow Queue described in [Concurrent Workflow Processing](configuring-performance.md#main-pars_title_15), except the Topics property matches the topic of your workflow jobs.

### CQ5 DAM Asset Synchronization Service
The `AssetSynchronizationService` is used to synchronize assets from mounted repositories (including LiveLink, Documentum, amongst others). By default this makes a regular check every 300 seconds (5 minutes), so if you do not use mounted repositories, you can disable this service.

This is done by [configuring the OSGi service](configuring-osgi.md) **CQ DAM Asset Synchronization Service** to set the **Synchronization period** ( `scheduler.period`) to (a minimum of) 1 year (defined in seconds).

### Multiple DAM instances
Deploying multiple DAM instances can help performance when, for example:

* you have a high load due to regular uploading of a large number of assets for the author environment; here a separate DAM instance can be dedicated to servicing author.
* you have multiple teams in world-wide locations (e.g. USA, Europe, Asia).

Additional considerations are:

* separating "work in progress" on author from "final" on publish
* separating internal users on author from external visitors/users on publish (e.g. agents, press representatives, customers, students, etc).

## Best Practices for Quality Assurance
Performance is of prime importance to your publish environment. Therefore, you need to carefully plan and analyze the performance tests you will make for the publish environment while implementing your project.

This section aims to give a standardized overview of the issues involved with defining a Test Concept specifically for performance tests on your *publish* environment. This is primarily of interest to QA engineers, project managers and system administrators.

The following covers a standardized approach to performance tests for a CQ application on the *Publish* environment. This involves the following 5 phases:

* [Verification of Knowledge](#VerificationofKnowledge)
* [Definition of Scope](#ScopeDefinition)
* [Test Methodologies](#TestMethodologies)
* [Definition of Performance Goals](#DefiningthePerformanceGoals)
* [Optimization](#Optimization)

Controlling is an additional, all-encompassing process - necessary but not limited to testing.

### Verification of Knowledge
A first step is to document the basis information which you need to know before you can start testing:

* the architecture of your test environment
* an application map detailing the internal elements which will need testing (both in isolation and combination)

#### Test Architecture
You should clearly document the architecture of the test environment being used for your performance testing.

You will need a reproduction of your planned production Publish environment, together with Dispatcher and Load Balancer.

#### Application Map
To get a clear overview you can create a map of the entire application (you may well have this from tests on the Author environment).

A diagram representation of the internal elements of the application, can give an overview of the testing requirements; with color-coding it can also act as a basis for reporting.

<!-- 

Comment Type: remark
Last Modified By: unknown unknown (remove-legacypath-6-1)
Last Modified Date: 2017-11-30T05:41:46.553-0500

<p>Missing verification map</p>

 -->

The example below illustrates the level of detail appropriate:

Verification Map

### Scope Definition
An application will usually have a selection of use cases. Some will be very important, others less so.

To focus the scope of the performance testing on publish, we recommend that you define the:

* most important business use cases
* most critical technical use cases

The number of use cases is up to you, but it should be limited to an easily manageable number (e.g. between 5 to 10).

Once the key use cases have been selected, then the key performance indicators (KPI) and the tools used to measure them can be defined for each case. Examples of common KPIs include:

* End to end response time
* Servlet response time
* Response time for a single component
* Response time for the services
* Number of idle threads in the thread pool
* Number of free connections
* System resources such as CPU and I/O access

### Test Methodologies
This concept has 4 scenarios used for defining and testing the performance goals:

* Single component tests
* Combined component tests
* *Going Live* scenario
* Error scenarios

Based on the following principles.

**Component Breakpoints**

* Each component has a specific breaking point when related to performance. This means that a component can show good performance until a specific point is reached, after which performance will degrade rapidly.   
* To get a full overview of the application, you must first verify your components to determine when the breakpoint of each is reached.   
* To find the breakpoint you can perform a load test where, over a period of time, you increase the number of users to create an increasing load. By monitoring this load, and the response of the components, you will encounter specific performance behavior when the breaking point of the component is reached. The point can be qualified by the number of concurrent transactions per second, together with the number of concurrent users (if the component is sensitive to this KPI).
* This information can then act as a benchmark for improvements, indicate the efficiency of the measures being used, and help define test scenarios.

**Transactions**

* The term transaction is used to represent the request of a complete web page, including the page itself and all subsequent calls; i.e. the page request, any AJAX calls, images and other objects.**Request Drill Down**
* To fully analyze each request you can represent each element of the call stack, then total the average processing time for each.

### Defining the Performance Goals
Once the scope, and related KPIs have been defined, the specific performance goals can be set. This involves devising test scenarios, together with target values.

You will need to test performance under both average and peak conditions. In addition, you will need Going Live scenario tests to ensure that you can cater for increased interest in your website when it is first made available.

Any experience, or statistics which you may have collected from an existing website can also be useful in determining future goals; for example top traffic from your live website.

#### Single Component Tests
Critical components will need to be tested - under both average and peak conditions.

In both cases, you can define the expected number of transactions per second when a predefined number of users are using the system.

| Component |Test Type |#Users |Tx/sec (Expected) |Tx/sec (Tested) |Description  |
|---|---|---|---|---|---|
| Homepage Single User |Average |1 |1 |  |  |
|   |Peak |1 |3 |  |  |
| Homepage 100 Users |Average |100 |3 |  |  |
|   |Peak |100 |3 |  |

#### Combined Component Tests
Testing the components in combination gives a closer reflection of the applications behavior. Again average and peak conditions must be tested.

| Scenario |Component |#Users |Tx/sec (Expected) |Tx/sec (Tested) |Description  |
|---|---|---|---|---|---|
| Mixed average |Homepage |10 |1 |  |  |
|   |Search |10 |1 |  |  |
|   |News |10 |2 |  |  |
|   |Events |10 |1 |  |  |
|   |Activations |10 |3 |  |Simulation of author behavior. |
| Mixed peak |Homepage |100 |5 |  |  |
|   |Search |50 |5 |  |  |
|   |News |100 |10 |  |  |
|   |Events |100 |10 |  |  |
|   |Activations |20 |20 |  |Simulation of author behavior. |

#### Going Live Tests
During the first few days after your website is made available, you can expect an increased level of interest. This will probably be even greater than the peak values you have been testing for. It is strongly recommended to test Going Live scenarios to ensure that the system can cater for this situation.

| Scenario |Test Type |#Users |Tx/sec (Expected) |Tx/sec (Tested) |Description  |
|---|---|---|---|---|---|
| Going Live peak |Homepage |200 |20 |  |  |
|   |Search |100 |10 |  |  |
|   |News |200 |20 |  |  |
|   |Events |200 |20 |  |  |
|   |Activations |20 |20 |  |Simulation of author behavior. |

#### Error Scenario Tests
Error scenarios must also be tested to ensure that the system reacts correctly and appropriately. Not only in how the error itself is handled, but the impact it may have on performance. For example:

* what happens when the user tries to input an invalid search term in the search box
* what happens when the search term is so general that it returns an excessive number of results

When devising these tests it should be remembered that not all scenarios will occur regularly. However, their impact on the entire system is important.

|  Error Scenario |Error Type |#Users |Tx/sec (Expected) |Tx/sec (Tested) |Description  |
|---|---|---|---|---|---|
| Search component overload |Search on global wildcard (asterisk) |10 |1 |  |Only &#42;&#42;&#42; are searched. |
|   |Stop word |20 |2 |  |Searching for a stop word. |
|   |Empty string |10 |1 |  |Searching for an empty string. |
|   |Special characters |10 |1 |  |Searching for special characters. |

#### Endurance Tests
Certain issues will only be encountered after the system has been running for a continuous period of time; be that either hours or even days. An endurance test is used to test an constant average load over a required period of time. Any performance degradation can then be analyzed.

| Scenario |Test Type |#Users |Tx/sec (Expected) |Tx/sec (Tested) |Description  |
|---|---|---|---|---|---|
| Endurance test (72 hours) |Homepage |10 |1 |  |  |
|   |Search |10 |1 |  |  |
|   |News |20 |2 |  |  |
|   |Events |10 |1 |  |  |
|   |Activations |1 |3 |  |Simulation of author behavior. |

### Optimization
In the later stages of implementation you will need to optimize the application to fulfill / maximize the performance goals.

Any optimizations made must be tested to ensure they have:

* not affected the functionality 
* been verified with the load tests before being released

A selection of tools is available to help you with load-generation, performance monitoring and/or results analysis:

* [JMeter](http://jakarta.apache.org/jmeter/)
* Load Runner (HP)
* [Determyne](http://www.determyne.com/) InsideApps
* [InfraRED](http://www.infraredsoftware.com/)
* [Java Interactive Profile](http://jiprof.sourceforge.net/)
* many more...

After optimization, you will need to test again to confirm the impact.

### Reporting
On-going reporting will be needed to keep everyone informed of the status; as mentioned previously with color-coding the Architecture Map can be used for this.

After all tests have been completed you will want to report on:

* any critical errors encountered
* non-critical issues which will still need further investigation
* any assumptions made during testing
* any recommendations to arise from the testing

## Optimizing Performance when using the Dispatcher
The [Dispatcher](/content/help/en/experience-manager/dispatcher/using/dispatcher) is Adobe's caching and/or load balancing tool. When using the Dispatcher you should consider optimizing your website for cache performance.

>[!NOTE]
>
>Dispatcher versions are independent of AEM, however the Dispatcher documentation is embedded in the AEM documentation. Always use the Dispatcher documentation that is embedded in the documentation for the latest version of AEM.
>
>You may have been redirected to this page if you followed a link to the Dispatcher documentation that is embedded in the documentation for a previous version of AEM.

The Dispatcher offers a number of built-in mechanisms that you can use to optimize performance if your website takes advantage of them. This section tells you how to design your web site to maximize the benefits of caching. 

>[!NOTE]
>
>It may help you to remember that the Dispatcher stores the cache on a standard web server. This means that you:
>
>* can cache everything that you can store as a page and request using an URL
>* cannot store other things, such as cookies, session data and form data.
>
>In general, a lot of caching strategies involve selecting good URLs and not relying on this additional data. 
>
>With Dispatcher version 4.1.11 you can also cache response headers, see [Caching HTTP Response Headers](/content/help/en/experience-manager/dispatcher/using/dispatcher-configuration#ConfiguringtheDispatcherCachecache).
>

#### Calculating the Dispatcher Cache Ratio
The cache ratio formula estimates the percentage of requests handled by the cache out of the total number of requests coming into the system. To calculate the cache ratio you need the following :

* The total number of requests. This information is available in the Apache `access.log`. For more details, see the [official Apache documentation](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* The number of requests the Publish instance served. This information is available in the `request.log` of the instance. For further details, see [Interpreting the request.log](monitoring-and-maintaining.md#Interpretingtherequestlog) and [Finding the log Files](monitoring-and-maintaining.md#FindingtheLogFiles).

The formula to calculate the cache ratio is:

* (The total number of requests **minus** the number of requests on Publish) **divided** by the total number of requests.

For example, if the total number of requests is 129491 and the number of requests served by the Publish instance is 58959 the cache ratio is: **(129491 - 58959)/129491= 54.5%**.

If you don't have a one to one publisher/dispatcher pairing, you will need to add requests from all dispatchers and publishers together to get an accurate measurement. See also [Recommended Deployments](recommended-deploys.md).

>[!NOTE]
>
>For best performance, Adobe recommends a cache ratio of 90% to 95%.

#### Using Consistent Page Encoding
With Dispatcher version 4.1.11 you can cache response headers. If you are not caching response headers on Dispatcher then problems can occur if you store page encoding information in the header. In this situation, when Dispatcher serves a page from the cache the default encoding of the web server is used for the page. There are two ways to avoid this problem:

* If you use only one encoding, make sure that the encoding used on the web server is the same as the default encoding of the AEM website.
* Use a `<META>` tag in the HTML `head` section to set the encoding, as in the following example:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Avoid URL Parameters
If possible, avoid URL parameters for pages that you want to cache. For example, if you have a picture gallery, the following URL is never cached (unless Dispatcher is [configured accordingly](/content/help/en/experience-manager/dispatcher/using/dispatcher-configuration#ConfiguringtheDispatcherCachecache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

However, you can put these parameters into the page URL, as follows: 

```xml
www.myCompany.com/pictures/gallery.christmas.1.html

```

>[!NOTE]
>
>This URL calls the same page and the same template as gallery.html. In the template definition, you can specify which script renders the page, or you can use the same script for all pages.

#### Customize by URL
If you allow users to change the font size (or any other layout customization), make sure that the different customizations are reflected in the URL.

For example, cookies are not cached, so if you store the font size in a cookie (or similar mechanism), the font size is not preserved for the cached page. As a result, Dispatcher returns documents of any font size at random.

Including the font size in the URL as a selector avoids this problem:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>For most layout aspects, it is also possible to use style sheets and/or client side scripts. These will usually work very well with caching.
>
>This is also useful for a print version, where you can use an URL such as: ``
>
>`www.myCompany.com/news/main.print.html`
>
>Using the script globbing of the template definition, you can specify a separate script that renders the print pages.

#### Invalidating Image Files Used As Titles
If you render page titles, or other text, as pictures, then it is recommended to store the files so that they are deleted upon a content update on the page:

1. Place the image file in the same folder as the page.
1. Use the following naming format for the image file:  
  
   `<page file name>.<image file name>`

For example, you can store the title of the page myPage.html in the file myPage.title.gif. This file is automatically deleted if the page is updated, so any change to the page title is automatically reflected in the cache.

>[!NOTE]
>
>The image file does not necessarily physically exist on the AEM instance. You can use a script that dynamically creates the image file. Dispatcher then stores the file on the web server.

#### Invalidating Image Files Used For Navigation
If you use pictures for the navigation entries, the method is basically the same as with titles, just slightly more complex. Store all the navigation images with the target pages. If you use two pictures for normal and active, you can use the following scripts:

* A script that displays the page, as normal.
* A script that processes ".normal" requests and returns the normal picture.
* A script that processes ".active" requests and returns the activated picture.

It is important that you create these pictures with the same naming handle as the page, to ensure that a content update deletes these pictures as well as the page.

For pages that are not modified, the pictures still remain in the cache, although the pages themselves are usually auto-invalidated.

#### Personalization
The Dispatcher cannot cache personalized data, so it is recommended that you limit personalization to where it is necessary. To illustrate why:

* If you use a freely customizable start page, that page has to be composed every time a user requests it.
* If, in contrast, you offer a choice of 10 different start pages, you can cache each one of them, thus improving performance.

>[!NOTE]
>
>If you personalize each page (for example by putting the user's name into the title bar) you cannot cache it, which can cause a major performance impact.
>
>However, if you have to do this, you can:
>
>* use iFrames to split the page into one part that is the same for all users and one part that is the same for all pages of the user. You can then cache both of these parts.
>* use client-side JavaScript to display personalized information. However, you have to make sure that the page still displays correctly if a user turns JavaScript off.
>

#### Sticky Connections
[Sticky connections](/content/help/en/experience-manager/dispatcher/using/dispatcher#TheBenefitsofLoadBalancing) ensure that the documents for one user are all composed on the same server. If a user leaves this folder and later returns to it, the connection still sticks. Define one folder to hold all documents that require sticky connections for the website. Try not to have other documents in it. This impacts load-balancing if you use personalized pages and session data.

#### MIME Types
There are two ways in which a browser can determine the type of a file:

1. By its extension (e.g. .html, .gif, .jpg, etc)
1. By the MIME-type that the server sends with the file.

For most files, the MIME-type is implied in the file extension. i.e.:

1. By its extension (e.g. .html, .gif, .jpg, etc)
1. By the MIME-type that the server sends with the file.

If the file name has no extension, it is displayed as plain text.

With Dispatcher version 4.1.11 you can cache response headers. If you do not cache response headers on Dispatcher be aware that the MIME-type is part of the HTTP header. As such, if your AEM application returns files that do not have a recognized file ending, and rely on the MIME-type instead, these files may be incorrectly displayed.

To make sure that files are cached properly, follow these guidelines:

* Make sure that files always have the proper extension.
* Avoid generic file serve scripts, which have URLs such as download.jsp?file=2214. Re-write the script to use URLs containing the file specification; for the previous example this would be download.2214.pdf.

## Backup Performance
This section presents a series of benchmarks used to assess the performance of CQ backups and effects of backup activity on application performance. The CQ backup presents a significant load on the system while it runs, and we measure this, as well as the effects of the backup delay settings that attempt to modulate these effects. The objective is to offer some reference data about the expected performance of backups in realistic configurations and quantities of production data, and to provide guidance about how to estimate backup times for planned systems.

### Reference Environment

#### Physical System

The results reported in this document were obtained from benchmarks run in a reference environment with the following configuration. This configuration is designed to be similar to a typical production environment in a data centre:

* H-P ProLiant DL380 G6, 8 CPUs x 2.533 GHz
* Serial attached SCSI 300GB 10,000RPM drives
* Hardware RAID controller; 8 drives in a RAID0+5 array
* VMware image CPU x 2 Intel Xeon E5540 @ 2.53GHz
* RedHat Linux 2.6.18-194.el5; Java 1.6.0_29
* Single Author instance running CQ 5.5 GM.

The disk subsystem on this server is quite fast, representative of a high performance RAID configuration that might be used in a production server. Backup performance can be sensitive to disk performance, and the results in this environment reflect performance on a very fast RAID configuration. The VMWare image is configured to have a single large disk volume which physically resides in local disk storage, on the RAID array.

The CQ configuration places the repository and datastore on the same logical volume, alongside all of the operating system and CQ software. The target directory for backups also resides on this logical filesystem.

#### Data Volumes
The following table illustrates the size of data volumes that are used in the backup benchmarks. The initial baseline content is first installed, then additional known amounts of data are added to increase the size of the content backed up. Back-ups will be created at specific increments to represent a large increase in content and what may be produced in a day. The distribution of content (pages, images, tags) will be roughly based on realistic production asset composition. Pages, images, and tags will be limited to a maximum of 800 child pages. Each page will include title, Flash, text/image, video, slideshow, form, table, cloud, and carousel components. Images will be uploaded from a pool of 400 unique files ranging in size from 37 kB to 594 kB.

| **Content** |**Nodes** |**Pages** |**Images** |**Tags** |
|---|---|---|---|---|
| Base install |69,610 |562 |256 |237 |
| Small content for incremental back-up |  
|+100 |+2 |+2 |
| Large content for full back-up |  
|+10,000 |+100 |+100 |

The backup benchmark is repeated with the additionnal content sets added at each repetition.

#### Benchmark Scenarios

The backup benchmarks cover two main scenarios: backups when the system is under significant application load, and backups when the system is idle. Although the general recommendation is that backups should be performed when the CQ system is as idle as possible, there are situations where it is necessary that the backup must be run when the system is under load.

Backup times and size of resulting backup are obtained from the CQ server logs. It is normally recommended that backups be scheduled for off-times when CQ is idle, such as in the middle of the night. This scenario is representative of the recommended approach.

Load will consist of page creates/deletes, traversals, and queries with the majority of load coming from page traversals and queries. Adding and removing too many pages continually increase the workspace size and prevent the back-ups from completing. The distribution of load the script will use is 75% page traversals, 24% queries and 1% page creations (single level with no nested sub-pages). Peak average transactions per second on an idle system is achieved with 4 concurrent threads, which is what will be used when testing back-ups under load.

Impact of load on backup performance can be estimated by the difference between performance with and without this application load. Impact of the backup on application throughput is found by comparing the scenario throughput in transactions per hour with and without a concurrent backup ongoing, and with backups operating with different "backup delay" settings.

### Summary of Results

#### Backup Time and Troughput
The main result of these benchmarks is to show how backup times vary as a function of the backup type and overall quantity of data. The following chart shows the backup time obtained using the default backup configuration, as a function of the number of total number of pages.

![](assets/configuring-performance/chlimage_1-4.png)

Backup times on an idle instance are fairly consistent, averaging 0.608 MB/s regardless of full or incremental backups (see chart below). The backup time is simply a function of the amount of data that is being backed up. The time to complete a full backup clearly increases with the total number of pages. The time to complete an incremental backup also climbs with the total number of pages, but at a much lower rate. The time taken to complete the incremental backup is much shorter owing to the relatively small amount of data being backed up.

The size of the backup produced is the main determinant of the time taken to complete a backup. The following chart shows time taken as a function of final backup size.

![](assets/configuring-performance/chlimage_1-5.png)

This chart illustrates that both incremental and full backups follow a simple size versus time pattern that we can measure as throughput. Backup times on an idle instance are fairly consistent, averaging 0.61 MB/sec regardless of full or incremental backups on the benchmark environment.

#### Backup Delay
The backup delay parameter is provided to limit the extent to which backups may interfere with production workloads. The parameter specifies a wait time in milliseconds, which is interspersed into the backup operation on a file-by-file basis. The overall effect depends partly on the size of files affected. Measuring backup performance in MB/sec gives a reasonable way to compare the effects of delay on the backup.

* Running a backup concurrently with regular application load will have a negative impact on the throughput of the regular load.
* The impact may be slight -- as little as 5% -- or could be very significant -- causing as much as 75% drop in throughput, and this likely depends on the application more than anything.
* Backup is not a heavy load on the CPU, and so CPU-intensive production workloads would be less affected by backup than I/O intensive ones.

![](assets/configuring-performance/chlimage_1-6.png)

For comparison the throughput obtained using a filesystem backup (using 'tar') to backup the same repository files. The performance of the tar is comparable, but slightly higher than the backup with delay set to zero. Setting even a small delay greatly reduces the backup throughput and the default delay of 10ms results in vastly reduced throughput. In situations where backups may be scheduled when overall application usage is very low or the application can be completely idle, it is probably desirable to reduce the delay below the default value in order to permit the backup to proceed more quickly.

The actual impact of application throughput of an ongoing backup does depend on the application and infrastructure details. The choice of delay value should be made by empirical analysis of the application, but should be chosen as small as possible, so that backups can complete as quickly as possible. Since there is only a weak correlation between the choice of delay value and the impact on application throughput, the choice of delay should favour shorter overall backup times, in order to minimize the overall impact of backups. A backup that takes 8 hours to complete, but affects throughput by -20% is likely to have a greater overall impact than one which takes 2 hours to complete but affects throughput by -30%.

### References

* [Administering - Backup and Restore](/content/help/en/experience-manager/6-4/sites/administering/using/backup-and-restore)
* [Managing - Capacity and Volume](/content/help/en/experience-manager/6-4/managing/using/best-practices-further-reference#CapacityandVolume)
