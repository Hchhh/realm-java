# Realm-Java : Create reactive mobile apps in a fraction of the time



<div align=center><img src="res\logo.png" alt="logo" style="zoom: 100%;" /><img src="res\contributor.png" alt="contributor" style="zoom: 100%;" /></div>

By main contributor [Christian Melchior]( https://github.com/cmelchior ) and other [83](https://github.com/realm/realm-java/graphs/contributors) contributors.

## Abstract

Realm is a fast and cross-platform mobile database, running directly inside phones, tablets or wearables and designed to be an alternative to 

Core Data and SQLite. The project was pioneered by ‘Y Combinator’ to make managing database easier and faster. Realm is an open source project living in GitHub and it is being maintained and developed by the core developers as well as quite a few external contributors. In this chapter Realm is analyzed in the following aspects: stakeholder analysis, context view, development view, technical debts, revolution perspective and conclusion. The chapter as a whole can serve as a helpful introduction to prospective developers looking to better understand the architecture to which they might contribute. (Lastly, we observe that Realm is a well-engineered project without glaring technical holes or major debt.)

## Table of Contents

**[1. Introduction](# Introduction)**

**[2. Stakeholder Analysis](#_Stakeholders)**

**[3. Context View](#_Context View)**

**[4. Development View](#_Development View)**

**5. Technical Debt**

**[6. Evolutional Perspective](# Evolutional Perspective)**

**7. Conclusion**

**8. Reference**

## Introduction

With the increasing use of the mobile devices such as phones, wearables and so on, the amount of data transferring between mobile devices grows exponentially every year, and the need for a database handling the data on mobile devices more efficiently is getting more intense. In 2014, the entrepreneurial team behind Y Combinator created Realm--The first database designed specifically for mobile platforms.

Realm is a cross-platform mobile database for iOS and Android, of which the core data engine is built in C++ instead of an ORM based on SQLite, so Realm is faster, better, and easier to use and accomplish database operations with less code than SQLite and CoreData. Besides, rather than simply encapsulating CoreData, Realm uses its own set of persistent storage engines. Furthermore, Realm is completely free, which makes it both more popular and more accessible to developers.

This chapter aims to give users a quick understanding of how Realm is organized, developed and maintained. Firstly, the Stakeholders and Context view are analyzed to provide insights into the organization of the project. Furthermore, detailed analysis of the architecture is presented in order to understand its structure. In addition, technical debt in terms of code, testing and documentation was also found throughout the analysis of the system and is presented in the chapter. This is followed by the evolution of the project explaining how Realm emerged from C++ and discussing the Realm which is considered as the alternative to CoreData and SQLite. Finally, the chapter is closed with the conclusion of the whole analysis.

## Stakeholders

As a MVCC (Multi-Version Concurrency Control) database which runs on mobile phone, pad and wearable devices, hundreds of developer was engaged in its development on [GitHub]( https://github.com/realm/realm-java ). Nowadays, it interacts with lots of stakeholders.

| **Stakeholders** | **Description**                                              | **Quality  Attributes Concerned** |
| ---------------- | ------------------------------------------------------------ | --------------------------------- |
| Acquirers        | Realm  is created by an entrepreneurial   team of Y-Combinator, who are  authorized funding for products and system development. | Usability,Reliability             |
| Assessor         | Rules  and regulations that apply to the  Realm product portfolio are handled by the General Management team. | Reliability,Usability,            |
| Communicators    | The Community Management team explains the system  with documentation and   training  materials. | Portability                       |
| Users            | Realm  is used by students,hobbyist as well as professions who want an excellent  database in the embedded system development. | Usability,Reliability,Portability |
| Testers          | All  bugs in the software can be posted on the Realm forum, emailed or issued on  GitHub. Bugs and problems are picked up  by the software and hardware staff    employees  of Realm or the contributors  on  GitHub. | Testability                       |
| Developers       | There  are both software and hardware teams working on the code for the end  products. | Modifiability                     |
| Support  Staff   | The website realm.io plays a    central role in staying in    touch with users that report bugs as well  as positive explanations about nice projects that can be built with the  products. | Usability,Reliability,Portability |
| Suppliers        | Realm  is created by core data engine C++ and provide its own data engine. We can  work with data objects directly and create database more efficiently. | Reliability                       |
| Maintainers      | Software  solutions are assessed by    the  Software development team in order to maintain the programming standards and  architectural choices. | Maintainability                   |

<div align=center><i>Fig.1 : Summary most important stakeholders<i/><div/>

On April 24th,2019 MongoDB announced that Realm had signed a final agreement for the acquisition, which is expected to be completed by January 31st, 2020. Dev Ittycheria, President and CEO of MongoDB, said: "Realm is very popular with mobile developers because it allows mobile developers to use data to accelerate innovation easily, which is very consistent with our philosophy.”

The power-interest grid is as followed:

<div align=center><img src="res\fig2.png" alt="logo" style="zoom: 80%;" /></div>
<div align=center><i>Fig.2 : Customers of Realm<i/><div/>

<div align=center><img src="res\fig3.png" alt="costumer" style="zoom: 70%;" /></div>
<div align=center><i>Fig.3 : Customers of Realm<i/><div/>



The acquisition of Realm will deepen MongoDB's relationship with the developer community focused on mobile and Server-Free development. Active developers using Realm have exceeded 100,000, and the solution has been downloaded more than 2 billion times. Realm currently has Realm database and Realm platform, which can help users deploy quickly and achieve seamless cloud data synchronization.

<div align=center><img src="res\fig4.jpg" alt="usage" style="zoom: 100%;" /></div>
<div align=center><i>Fig.4 :Wild usage of Realm<i/><div/>


Now Realm is still trying its best to communicate with the latest and hot technical aspects, such as 5G, IBM Cloud Functions, Microsoft Azure and so on. The group of stakeholders will become more and more powerful, as well as its bright future.

## Context View

The context view shows the different relations, dependencies and interactions Realm has with its environment. Important for the context are the people, systems and external entities with which the system interacts.

### **System Scope & Responsibilities**

According to its website, Realm Database is defined as a “**fast, easy to use, and open source alternative to SQLite and Core Data for IOS and Android developers today**”. The scope of the software is clearly defined here. It is a database engine utilizing many new features (e.g. offline functionality, data synchronization, etc.) on mobile platforms, which are IOS and Android.

And the responsibilities define what the system should do in order to fulfill its objective. These include the following:

- l Employing features of offline-first functionality, fast queries and safe threading.

- l Providing powerful encryption that is strong enough for global financial institutions.

- l Providing seamless data synchronization with the aid of Realm Platform. 

- l Enabling users to build reactive apps with live objects, which means they always have the latest data.

- Open source on GitHub, allowing add-ons from open community.

### **External Entities**

​         Realm Java is a widely-used mobile database out of Y Combinator Inc. As one can imagine, a software project like this cannot be developed without external libraries, tools and frameworks. On the other, many companies cannot develop their software without Realm Java. These external relations are examined in this section.  

<div align=center><img src="res\fig5.png" alt="logo" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.5 :External Entities<i/><div/>

In order to understand the context model of Realm Java, the role of the external entities with respect to Realm Java is explained.


- **Programming Languages & Supported Platforms & IDE**

  Realm Java is now available only on the Android platform. Given that, Android Studio is the one IDE that users working with Realm Java should work on. Accordingly, no programming language but Java is allowed. The software of Android Studio can be installed on multiple platforms: Linux, Mac OS and Windows.

-  **Developers**

  The very first version of Realm was written in C++ by a development team From San Francisco. Soon, new versions of Realm written in other mainstream languages are developed with the help of open source community. Realm Java, for example, is now maintained by the combined effort from Realm team and individual developers on GitHub.

-  **Development Tools**

  As is mentioned above, Realm Java requires specific development tools such as Java SDK and Android Studio. Also, there are tools developed by Realm team to operate on Realm database. Realm Studio helps users open and edit local and synced Realms, and administer any RealmServer instance. Realm Browser, which is available only on Mac OS, shares the same abilities. 

- **Users**

  Thanks to its powerful features, Realm Java is widely used in all kinds of trades. For example, Cartasite built an offline-first app for heavy industries that seamlessly syncs field data with backend system, and Tread Learning uses Realm Platform to help special education teams coordinate care by syncing data in realtime across multiple devices. After all, Realm is built into apps used by hundreds of millions of people every day.

- **Version control and Issue Tracker**

  Realm Java uses GitHub and Git for version control to help developers collaborate and track issues related to the software. Contributions in this repository come from the Realm Java development team, as well as from open source community.  

- **Competitors**

  Main competitors in the field of mobile app database is SQLite and Core Data, which have considerably large user base. According to Realm website, however, Realm database outweighs its competitors in many aspects.  

- **Communication Tools**

  In order to stay in contact with developers and users, the following communication tools are used: the Realm Website, the Realm Forum. Also, using Git, individual developers can communicate with Realm team on a technical level. What’s more, Realm’s community managers also need to maintain a good relationship with magazines like ADT Magazine who writes about Realm products and competitors.

### Quality Attributes

#### **Runtime System Qualities**

##### **Functionality**

- Employing features of offline-first functionality, fast queries and safe threading.

- Providing powerful encryption that is strong enough for global financial institutions.

- Providing seamless data synchronization with the aid of Realm Platform. 

- Enabling users to build reactive apps with live objects, which means they always have the latest data.

##### **Performance**

***Scenario***: Realistic limits of storing declared by Realm Doc are violated.

***Source of Stimulus***: Users

***Stimulus***: Inappropriate ways of storing information

***Artifact***: System

***Environment***: Under normal operations

***Response***: Presenting warnings and errors 

##### **Security**

***Scenario***: Hackers attack the database and attempt to steal information stored.

***Source of Stimulus***: Hackers

***Stimulus***: Attempts to steal stored information

***Artifact***: Data stored in the database 

***Environment***: Whether users are online or offline

***Response***: Verify visitors’ identification through a symmetric key (AES)

##### **Availability**

***Scenario***: Possible mistakes made by users when building app with Realm database.

***Source of Stimulus:*** Users

***Source of Stimulus:*** Users

***Stimulus:*** System crash due to users’ mistakes

***Artifact:*** Component that dealing with crashes

***Environment***: Under normal operations

***Response***: Record the crash information and inform the parties concerned

##### **Usability**

***Scenario***: Users are unfamiliar with the configuration steps and want to learn them.

***Source of Stimulus***: Users

***Stimulus***: Attempt to learn about configuration steps and system features

***Artifact***: System

***Environment***: During configuration

***Response***: Provide links to help documents 

#### **Non-Runtime Qualities**

##### **Modifiability**

***Scenario:*** Developers in open source community have better ideas to help improve the Realm Java Project.

***Source of Stimulus:*** Developers in open source community

***Stimulus:*** Commitments of modifications of Realm Java source code.

***Artifact:*** System

***Environment:*** During designing

***Response:*** Test the modifications and deploy them.

##### **Integrability**

***Scenario:*** Users have demand of integrating Realm with other commonly used libraries for Android.

***Source of Stimulus:*** Users

***Stimulus:*** Importing of external libraries.

***Artifact:*** System

***Environment:*** During compiling

***Response:*** Link with external libraries.

##### **Testability**

***Scenario:*** Users need to test the apps developed in Realm Java unit by unit.

***Source of Stimulus:*** Users

***Stimulus:*** Completed unit 

***Artifact:*** Component being tested

***Environment:*** During developing

***Response:*** Prepare testing environment and provide results.

#### **Architecture Qualities**

##### **Conceptual Integrity**

- The whole point of Realm, or at least one of its very core ideas, is that it is objects all the way down.
- Try to minimize overhead.
- Try to keep as many operations as zero-copy as possible.

## Development View

### Module organization

Obviously, realm-java is composed of a large quantity of source files,which are logically organized into disparate modules. We have made a module organization for getting a much clearer understanding of the whole realm-java project.

A module organization describes how the organization of the source files classified into modules that contain related code. Such a structure provide an overview of the source code which guides developers to understand and navigate the codebase.

All main modules are described in the table below .

| **Module**   | **Description**                                              |
| ------------ | ------------------------------------------------------------ |
| Test         | All the test-related files.                                  |
| Exceptions   | Classes  for exceptions and errors,stack trace removing logic,cleaning public APIs. |
| JUnit        | Realm-java JUnit integration,rule and  runners,and JUnit integration support classes. |
| Listener     | Public  classes related to the listener APIs.                |
| Handler      | Classes  calling all listeners wanted for the realm-java, before delegating it to the  parameterized handler. |
| Runners      | JUnit  runners,internal classes and utils for runners implementation. |
| Session      | Realm-java session builder and  implementation.              |
| Verification | Verification  checkers, implementations for dealing with matching arguments,verification  logic and implementation. |
| Creation     | Classes for realm object creation including its settings, instances. |
| Debugging    | Everything  which helps debugging failed testss              |
| Util         | All the static utils including reflection utilities, IO utils, and so on. |
| Invocation   | Public  API related to realm method invocations,invocation related classes, and  implementations of method calls. |
| Plugins      | Plug-in components realm use in the  process of compiling.   |
| Transaction  | Encapsulate  a realm transaction.                            |
| Annotations  | Annotations realm use to mark the field  or classes.         |
| Progress     | Class used to encapsulate progress notifications when  either downloading or uploading Realm data. |
| Session      | Realm session builder and implementation.                    |
| Migration    | Classes used to perform the migration of one realm  schema to another. |
| Schema       | Class for interacting with the schema for a given `RealmObject` class. |
| UserStore    | Interface for classes responsible for saving and  retrieving Object Server users again. |

<div align=center><i>Fig.6 :description of the main modules<i/><div/>

All modules interact together to implement the function of Realm-java. In table 2, we can find out the modules into which the individual source files are collected and e dependency among these modules, and only the main part of the project is shown.

<div align=center><img src="res\fig7.png" alt="main part" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.7 :main part of the project<i/><div/>


Access layer - Provide external support of Realm-java. Through Gradle or Maven, users can access Realm-java as a library for project.

Interface layer - Interfaces for the internal layer,including exceptions interface, configuration interface, `UserStore` interface,session,migration and so on.

Internal layer - All the main classes in Realm-java are functioned, including `exceptions`, `configuration`,`userstore`, `transaction`, `session`, and so on.

Platform - All the external and basic libraries for internal layer,including Java standard library and JUnit.

### Common Design Models

In this section, common designs that are used and standardized in the development of Realm are described.

#### Common Process Standardization

As a MVCC Database,Realm in Java has some common used models to follow. First of all,it must run on Android platform. Java other than Android is not currently supported. Meanwhile, the version of Android studio must be above 1.5.1 and the version of SDK must be updated. JDK should also be above Version 7.It also supports Android 2.3 and the later.

To configure the Realm,`RealmConfiguration` present with some methods:

- `Builder.name`: Specifies the name of the database. If not, it is default.

- `Builder.schemaVersion`: Specify the version number of the database.

- `Builder.encryptionKey`: Specify the key for the database.

- `Builder.migration`: Specify the migration class for the migration operation.

- `Builder.inMemory`: Declare database persistent only in memory.

- `build`: Finish configuration。

#### Design Standardization

For Realm is an open source platform, everyone is free to contribute to the repository on GitHub. Seeing as multiple contributors are influencing Realm, the core developers have standardized aspects of the design of the  system to make it as maintainable, reliable and technically cohesive as possible. The most important aspects of contributing to Realm are discussed in the [Realm Platform Extensions License](https://github.com/realm/realm-java/blob/master/LICENSE) part on GitHub:

- Contributors are Licensors and any individual or Legal Entity on behalf of whom a contribution has been received by Licensor and subsequently incorporated within the work;

- Unless contributors explicitly state otherwise,any contribution intentionally submitted for inclusion to the Licensor shall be under the terms and conditions of the License, without any additional terms or conditions;

- When contributors reproduce and distribute copies of the work or derivative works thereof in any medium, with or without modification,they must present modified files to carry prominent notices stating that they changed the files.

#### Test Standardization

By standardizing the test approaches, technologies and conventions, the overall testing process remains consistent and has a  higher pace. Realm has a standardized fold Tests which contains all kinds of tests needed in the development.

File `Configuration/Realm/Tests.xcconfig` is to configure the test code and locate to `Realm/Tests/RealmTests-Info.plist`,which contains test information such as `Query tests`, `property tests`, `object tests` and so on will execute to test the modified codes. Thus, the contribution can be merged into the process when build succeeds.

### Codeline Module

## 

<div align="center"><img src = "res\fig8.png" alt="file structure" style="zoom: 90%;"></div> <div align=center><i>Fig.8 : file structure of Realm<i/><div/>

The core of Realm-Java is partitioned into following parts, and we will discuss them in the following part :

- **realm** : contains the key code in Java and Kotlin.
- **realm-annotations** : contains the added annotations in Realm.
- **realm-transformer** : take part in compilation to generate code.

### realm

Folders underneath the *realm* folder:

- **kotlin-extensions**

  This folder contains code in Kotlin that provides Realm functionality in a Kotlin program.  For example, in the code of file `RealmModelExtension`, it presents many functions such as `deleteFromRealm()`, `isValid()`, `isLoaded()` etc. These functions can be called in a Kotlin program to create or edit Realm Object. 

- **realm-annotations-processor**

  Code in this folder plays the role of annotation processor in Java. The Realm annotations are explained in the following part. `annotations-processor` explain itself literally. 

- **realm-library**

  <div align="center"><img src = "res\fig9.png" alt="realm-library" style="zoom: 60%;"></div> <div align=center><i>Fig.9 : file structure of realm-library<i/><div/>

  This is the core folder containing the functional code of Realm. `androidTest` folder contains file that make example of a given function in applying Realm. The purposes of each tests are revealed by its name literally. code in `androidTestObjectServer` test Realm `objectServer`.  Deploying a server object allows programmers to run realm remotely. `testUtils` contains code that are for test as well. The core part of Realm is encapsulated in the `main` folder.  Two folders are located underneath this folder: `cpp` and `java`.  `cpp` folder contains code mainly for compilation, and code in Java makes up the core of Realm, such as defining `RealmObject`, `Realm Error`, `Realm Collection` etc., and make base classes such as `BaseRealm`, `RealmList` etc.

- other folders

  Auto generated folders are listed in this classification, such as `config`, `gradle`, `tools` etc.

### realm-annotation

Code under this folder create annotations for realm, which usually work with annotation-processor we mentioned before. Several annotations are created here, such as: `RealmField`, `RealmClass`, `PrimaryKey` etc. Annotation are special tags in the proxy that can be read and processed at compile, loading class, and run-time starting with JDK5. By using annotations, developers can embed additional information in the source file without changing the original logic. This makes sense in Realm, since Realm provides many functions and attributes for developers so that developers don't need to do extra work for the object they have to declare manually. The reason why programmers benefit from the simplicity of such usage lies in the code underneath this folder. On the other hand, another use of this folder is to keep the code written by the programmers in accordance both logically and grammatically.

### realm-transformer

This part has three key Java files: `ComputerIdentifierGenerator`, `RealmAnalytics`, `Utils`, which plays an important role in helping Realm generate code during compilation.



## Evolutional Perspective

The evolution perspective deals with concerns related to evolution during the lifetime of a system, which is relevant to Realm for it need to be changing continuously along with the coding language and developing tools.

Realm has changed significantly since its first draft in 2014-09-29. Its initial intension was to build a mobile database which is faster and safer than the existing one such as SQLite etc. However, five years from then, Realm has done much more than that. It supports not only Android, but Swift, JavaScript, .Net other platforms as well. It’s an embedded database which provides developers a distinct way to treat modules and their service logics. All notable changes to the project are documented in the [CHANGELOG.md](https://github.com/realm/realm-java/blob/master/CHANGELOG.md).

The first draft version is 0.71.0, released in 2014. After the first version, various changes have been made, which were either to fix bugs or to add new features. The first breaking release took place in 2015-10-08. This release announced that the current Realm files no longer support previous ones, and many deprecated functions, methods, and constructors from the Realm class were removed. The most noteworthy one is that boxed type such as Boolean, Byte, Short, Integer, Long, Float and Double were introduced to the Realm class. Additionally, from now on, Realm adds support for x86-64. Other bug fixing job has done in this version as well. 

<div align=center><img src="res\fig10.jpg"  alt="ver1" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.10 :Realm Version 0.88.0 prerequisite<i/><div/>



Five months later, in 2016-03-10, Realm has released version 0.88.0. In this version Realm has to be installed as a Gradle plugin, which means it relies on Android Studio from now on, and do not support Java outside of Android. This means that Realm in Java has a tighter bonding relationship with Android Studio, which indicates it has a bigger potential to be applied in an Android Operating System mobile device.

<div align=center><img src="res\fig11.jpg" alt="ver2" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.11 :Realm Version 2.0.0<i/><div/>



In 2016-09-27, Realm released the version of 2.0.0. As we can see, within 2 years, Realm has released two upward compatible versions. On the one hand, we have to admit that, with the increasing amount of software engineers joining into the project, as well as the popularity of the development of ‘light database’, Realm has made great breakthroughs and provided convenience for mobile software development. However, on the other hand, frequent forward upgrades increase the instability of the whole system. The new release also added many features, such as added new `RealmFileException` etc. However, Realm 2.0.0 contained a serious bug ‘Build error when using Java 7’ which would cause serious problem for programmers for Java 7 is still the latest version back then, and was not finished until version 2.0.2.

<div align=center><img src="res\fig12.jpg" alt="ver2" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.12 :Realm Version 4.0.0<i/><div/>

For almost two years, programmers have been using Realm from version 2.X.0 to 3.X.0. Realm has made a lot of changes during this period but not as noteworthy until the release of version 4.0.0 in 2017-10-16. In Realm 4.0.0, The internal file format has been upgraded, which means opening an older Realm will upgrade the file automatically, but older versions of Realm will no longer be able to read the file. Additionally, Realm upgraded a series of Internal components to adapt to the current version. 

<div align=center><img src="res\fig13.jpg" alt="ver2" style="zoom: 100%;" /></div>
  <div align=center><i>Fig.13 :Realm Version 5.0.0<i/><div/>

Half a year later, Realm 5.0.0 was released in 2018-03-15. This release is compatible with the Realm Object Server 3.0.0-beta.3 or later.

The latest version is Realm 5.15.1, which was released in 2019-09-09, and the lead developers are still making progress for new version. The project is published on [GitHub](https://github.com/realm/realm-java), which is still an active project. This is necessary, considering Realm is intended to replace SQLite as a mobile database.