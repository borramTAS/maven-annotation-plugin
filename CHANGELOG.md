# Maven Annotation Plugin - Changelog

<!-- Changelog for bsorrentino maven-annotation-plugin. -->

<<<<<<< HEAD
## 4.1-jdk8
=======
## v4.4
>>>>>>> master
### Generic changes

**move to next release version**


[a85380b0a634c9c](https://github.com/bsorrentino/maven-annotation-plugin/commit/a85380b0a634c9c) bsorrentino *2020-07-30 15:39:58*

**move next dev version**


[5039031bff9b910](https://github.com/bsorrentino/maven-annotation-plugin/commit/5039031bff9b910) bartolomeo sorrentino *2020-07-30 15:19:42*


<<<<<<< HEAD
###  [#82](https://github.com/bsorrentino/maven-annotation-plugin/issues/82) New v4.0 does not support Java 8    *bug*  *under investigation*  

**issue #82 - fix 'UnsupportedOperationException' on isSupportedOption invocation**

=======
[fa1f52af0d550c9](https://github.com/bsorrentino/maven-annotation-plugin/commit/fa1f52af0d550c9) bartolomeo sorrentino *2020-10-01 14:47:42*

**set release version**


[1714e8977800c50](https://github.com/bsorrentino/maven-annotation-plugin/commit/1714e8977800c50) bartolomeo sorrentino *2020-10-01 14:47:30*

**refine integration test**


[692074de91c1440](https://github.com/bsorrentino/maven-annotation-plugin/commit/692074de91c1440) bartolomeo sorrentino *2020-10-01 14:30:14*

**update debug message**


[9646e901989224d](https://github.com/bsorrentino/maven-annotation-plugin/commit/9646e901989224d) bartolomeo sorrentino *2020-10-01 14:29:27*

**Start work on 4.4-SNAPSHOT**


[cb7191dfff79390](https://github.com/bsorrentino/maven-annotation-plugin/commit/cb7191dfff79390) Martijn Dashorst *2020-09-27 12:51:35*

**update changelog**


[b5bee16c5832f6f](https://github.com/bsorrentino/maven-annotation-plugin/commit/b5bee16c5832f6f) bsorrentino *2020-09-25 15:59:25*


###  [#86](https://github.com/bsorrentino/maven-annotation-plugin/issues/86) File change detection doesn&#39;t detect removals  

**Detects file additions/deletions for skipping**

 * When you remove a file from the source tree, the modification checker
 * doesn&#39;t take into account the removed file as an update. Because the
 * file no longer exists, it doesn&#39;t have a modification date, and it will
 * not count in determining whether the last generation was older than the
 * modification in the sources.
 * This commit detects source file modifications of the nature of
 * additions and deletions by using a tracking file in the output folder
 * (`.maven-processor-source-files.txt`).
 * This file contains a list of all the files in the source folders, which
 * is checked against the current list of source files. When the file
 * doesn&#39;t exist or if the sets of files don&#39;t match, it is treated as a
 * change. When they match exactly, the modification time check is still
 * run.
 * A sample run without additions/removals in the source files:
 * ```
 * [DEBUG]   (f) skipSourcesUnchanged = true
 * [DEBUG]   (f) sourceDirectory = /Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java
 * [DEBUG] -- end configuration --
 * [DEBUG] Source directory: /Users/dashorst/IdeaProjects/iridium/common/entities/target/generated-sources/apt added
 * [DEBUG] processing source directory [/Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java]
 * [DEBUG] removed source files: []
 * [DEBUG] new source files: []
 * [DEBUG] max source file date: 1601210991895, max output date: 1601211873845
 * [INFO] no source file(s) change(s) detected! Processor task will be skipped
 * ```
 * When a file was removed:
 * ```
 * [DEBUG]   (f) skipSourcesUnchanged = true
 * [DEBUG]   (f) sourceDirectory = /Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java
 * [DEBUG] -- end configuration --
 * [DEBUG] Source directory: /Users/dashorst/IdeaProjects/iridium/common/entities/target/generated-sources/apt added
 * [DEBUG] processing source directory [/Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java]
 * [DEBUG] removed source files: [/Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java/nl/topicus/platinum/entities/Afdeling.java]
 * [DEBUG] new source files: []
 * [WARNING] No processors specified. Using default discovery mechanism.
 * [DEBUG] javac option: -cp
 * ```
 * When the file is re-added:
 * ```
 * [DEBUG]   (f) skipSourcesUnchanged = true
 * [DEBUG]   (f) sourceDirectory = /Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java
 * [DEBUG] -- end configuration --
 * [DEBUG] Source directory: /Users/dashorst/IdeaProjects/iridium/common/entities/target/generated-sources/apt added
 * [DEBUG] processing source directory [/Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java]
 * [DEBUG] removed source files: []
 * [DEBUG] new source files: [/Users/dashorst/IdeaProjects/iridium/common/entities/src/main/java/nl/topicus/platinum/entities/Afdeling.java]
 * [WARNING] No processors specified. Using default discovery mechanism.
 * [DEBUG] javac option: -cp
 * ```
 * Fixes #86

[1f6c708506ea959](https://github.com/bsorrentino/maven-annotation-plugin/commit/1f6c708506ea959) Martijn Dashorst *2020-09-27 13:10:57*


## v4.3
### Generic changes

**update readme**


[382dfb7fe61851a](https://github.com/bsorrentino/maven-annotation-plugin/commit/382dfb7fe61851a) bsorrentino *2020-09-25 15:31:42*

**set release version**


[db87a0476c03596](https://github.com/bsorrentino/maven-annotation-plugin/commit/db87a0476c03596) bsorrentino *2020-09-25 15:28:27*

**Start 4.3-SNAPSHOT development**


[be4e8404052f7e6](https://github.com/bsorrentino/maven-annotation-plugin/commit/be4e8404052f7e6) Martijn Dashorst *2020-09-23 09:37:39*

**Implement lastModified check for sources**

 * The annotation processor should be able to skip the annotation
 * processing if the sources haven&#39;t changed since the last processing.
 * This will speed up project builds considerably since for example the
 * JPA metamodel generator will not run if the entities haven&#39;t been
 * modified, which will save the compiler of having to recompile your
 * whole module.
 * Using the option `skipWithoutSourceChanges` you can enable this
 * behavior. By default it is turned off to maintain the current behavior.
 * This change doesn&#39;t track individual files, as there need not be a 1-1
 * mapping between the origin of the annotation processor and the
 * generated sources. The plugin rather determines from all source
 * locations what the most recent last modified time is, and does the same
 * for all the files in the output folder.
 * This cuts down rebuild times on my current project by a half or so
 * (going from over 2 minutes to just 1 minute).

[30861dbad2fef67](https://github.com/bsorrentino/maven-annotation-plugin/commit/30861dbad2fef67) Martijn Dashorst *2020-09-23 09:37:39*

**uodate site-maven-plugin version**


[c6dbeb9bb1e5709](https://github.com/bsorrentino/maven-annotation-plugin/commit/c6dbeb9bb1e5709) bsorrentino *2020-08-05 16:15:28*


###  [#85](https://github.com/bsorrentino/maven-annotation-plugin/pull/85) Utilize lastModified times of source and output to skip annotation processing    *work in progress*  

**merged PR #85**

 * renamed property from &#39;skipWithoutSourceChanges&#39; to &#39;skipSourcesUnchanged&#39;
 * put PR code in a new method &#39;isSourcesUnchanged( List&lt;&gt; allSources )&#39;

[2bf7bedb068e64d](https://github.com/bsorrentino/maven-annotation-plugin/commit/2bf7bedb068e64d) bsorrentino *2020-09-24 10:03:51*


## v4.2
### Generic changes

**update changelog**


[e0e7553ab7126cd](https://github.com/bsorrentino/maven-annotation-plugin/commit/e0e7553ab7126cd) bsorrentino *2020-08-03 14:18:25*

**update readme**


[86b4a9ba0a77deb](https://github.com/bsorrentino/maven-annotation-plugin/commit/86b4a9ba0a77deb) bsorrentino *2020-08-03 14:18:00*

**move to next release version**


[450b98cc62f42d9](https://github.com/bsorrentino/maven-annotation-plugin/commit/450b98cc62f42d9) bsorrentino *2020-08-03 14:13:45*

**clean code**


[ac57d4884350a9c](https://github.com/bsorrentino/maven-annotation-plugin/commit/ac57d4884350a9c) bsorrentino *2020-07-31 09:35:06*

**move to next developer version**


[08235617ae9b1d2](https://github.com/bsorrentino/maven-annotation-plugin/commit/08235617ae9b1d2) bsorrentino *2020-07-31 08:28:15*

**update readme**


[13aa52ade58dcae](https://github.com/bsorrentino/maven-annotation-plugin/commit/13aa52ade58dcae) bsorrentino *2020-07-31 08:00:05*


###  [#83](https://github.com/bsorrentino/maven-annotation-plugin/issues/83) &#39;process-test&#39; does not add TestCompileSourceRoots to javac &#39;-sourcepath&#39;    *bug*  *wait for feedback*  *work in progress*  

**fix: process-test should add CompileSourceRoots and TestCompileSourceRoots to javac '-sourcepath' option. fixes #83**


[2f1380abc231c26](https://github.com/bsorrentino/maven-annotation-plugin/commit/2f1380abc231c26) Markus *2020-07-30 15:59:55*


## v4.1
### Generic changes

**move to next release version**


[7939e7348408ffb](https://github.com/bsorrentino/maven-annotation-plugin/commit/7939e7348408ffb) bsorrentino *2020-07-31 07:40:09*

**update readme**


[18df0d926c9a3f1](https://github.com/bsorrentino/maven-annotation-plugin/commit/18df0d926c9a3f1) bartolomeo sorrentino *2020-07-23 08:21:15*
>>>>>>> master

[3a072bfb140ae3c](https://github.com/bsorrentino/maven-annotation-plugin/commit/3a072bfb140ae3c) bartolomeo sorrentino *2020-07-28 13:31:23*


## 4.0-jdk8
### Generic changes

**update change log**


[2e0c812c1e1a7d8](https://github.com/bsorrentino/maven-annotation-plugin/commit/2e0c812c1e1a7d8) bartolomeo sorrentino *2020-07-22 08:59:18*

**set release version**


[99669c06ab305dd](https://github.com/bsorrentino/maven-annotation-plugin/commit/99669c06ab305dd) bartolomeo sorrentino *2020-07-22 08:56:11*

**add test module**


[3db821f8c8e7225](https://github.com/bsorrentino/maven-annotation-plugin/commit/3db821f8c8e7225) bartolomeo sorrentino *2020-07-22 08:45:24*

**move to next developer version**


[a813a22cee3f82e](https://github.com/bsorrentino/maven-annotation-plugin/commit/a813a22cee3f82e) bartolomeo sorrentino *2020-07-20 08:01:04*

**update readme**


[4c80b26d89676ba](https://github.com/bsorrentino/maven-annotation-plugin/commit/4c80b26d89676ba) bartolomeo sorrentino *2020-07-20 07:57:39*

**remove default source and target compiler option**


[5ef8f3b48474e13](https://github.com/bsorrentino/maven-annotation-plugin/commit/5ef8f3b48474e13) bartolomeo sorrentino *2020-04-16 23:55:38*

**add maven enforcer**


[8efac77492e7274](https://github.com/bsorrentino/maven-annotation-plugin/commit/8efac77492e7274) bartolomeo sorrentino *2020-04-16 22:24:57*

**move to next developer version**


[785c31b31785d2f](https://github.com/bsorrentino/maven-annotation-plugin/commit/785c31b31785d2f) bsorrentino *2020-03-02 19:59:10*

**update changelog**


[42d5623ace037c2](https://github.com/bsorrentino/maven-annotation-plugin/commit/42d5623ace037c2) bartolomeo sorrentino *2020-03-02 19:02:33*

**update ignore**


[0d2cb8114432cbd](https://github.com/bsorrentino/maven-annotation-plugin/commit/0d2cb8114432cbd) bartolomeo sorrentino *2020-03-02 18:59:31*

**add changelog support**


[57b41626d1e6ab3](https://github.com/bsorrentino/maven-annotation-plugin/commit/57b41626d1e6ab3) bsorrentino *2020-02-26 02:30:48*

**move to next developer version**


[abd261ca0b3e498](https://github.com/bsorrentino/maven-annotation-plugin/commit/abd261ca0b3e498) bsorrentino *2020-02-24 23:31:45*

**move to next developer version**


[6b5f170872c766f](https://github.com/bsorrentino/maven-annotation-plugin/commit/6b5f170872c766f) bsorrentino *2020-02-24 23:23:43*

**update ignore**


[03482b5e2d2f909](https://github.com/bsorrentino/maven-annotation-plugin/commit/03482b5e2d2f909) bsorrentino *2020-02-24 23:21:23*

**update ignore**


[23cfeff0350f118](https://github.com/bsorrentino/maven-annotation-plugin/commit/23cfeff0350f118) Bartolomeo Sorrentino *2019-04-23 15:36:20*

**modernize code**


[5cc364404c3ba1c](https://github.com/bsorrentino/maven-annotation-plugin/commit/5cc364404c3ba1c) Bartolomeo Sorrentino *2019-04-23 15:36:10*

**update pom for next major release**


[0f00f5860ba309f](https://github.com/bsorrentino/maven-annotation-plugin/commit/0f00f5860ba309f) Bartolomeo Sorrentino *2019-04-23 15:28:09*

**override method addModules in javax.tools.JavaCompiler.CompilationTask**


[b7434e5617baa16](https://github.com/bsorrentino/maven-annotation-plugin/commit/b7434e5617baa16) bsorrentino *2019-04-12 15:07:59*

**update readme**


[8065847d06dde32](https://github.com/bsorrentino/maven-annotation-plugin/commit/8065847d06dde32) bsorrentino *2018-08-12 13:56:30*


###  [#79](https://github.com/bsorrentino/maven-annotation-plugin/issues/79) move to java9    *enhancement*  

**#79 add maven shell in docker**


[8000153b4e6b00a](https://github.com/bsorrentino/maven-annotation-plugin/commit/8000153b4e6b00a) bartolomeo sorrentino *2020-03-02 19:00:40*

**#79 update readme**


[41242f465f6b338](https://github.com/bsorrentino/maven-annotation-plugin/commit/41242f465f6b338) bartolomeo sorrentino *2020-03-02 18:58:10*

**#79 add docker to test jdk version**


[afcff71d8a5b9f4](https://github.com/bsorrentino/maven-annotation-plugin/commit/afcff71d8a5b9f4) bartolomeo sorrentino *2020-03-02 18:56:28*

**issue #79**

 * make multimodule project

[3ec2718dfe15dab](https://github.com/bsorrentino/maven-annotation-plugin/commit/3ec2718dfe15dab) bsorrentino *2020-02-26 03:37:03*

**issue #79**

 * code refactoring
 * update source / target to java 9
 * upgrade dependencies

[f84460766d58da5](https://github.com/bsorrentino/maven-annotation-plugin/commit/f84460766d58da5) bsorrentino *2020-02-26 02:09:21*


###  [#80](https://github.com/bsorrentino/maven-annotation-plugin/issues/80) How to exclude module-info.java file?  

**issue #80**

 * add support for -source and -target compiler options that are filled by maven.compiler.* properties

[18212a3518d162e](https://github.com/bsorrentino/maven-annotation-plugin/commit/18212a3518d162e) bartolomeo sorrentino *2020-04-17 15:32:19*

**issue #80**

 * add support of javac option --module-path

[8d6d9c34e0c5722](https://github.com/bsorrentino/maven-annotation-plugin/commit/8d6d9c34e0c5722) bartolomeo sorrentino *2020-04-16 23:37:10*


###  [#81](https://github.com/bsorrentino/maven-annotation-plugin/issues/81) Compilation errors ignored during processing    *under investigation*  

**issue #81 add compilation result**


[85ba56d3b87e40a](https://github.com/bsorrentino/maven-annotation-plugin/commit/85ba56d3b87e40a) bartolomeo sorrentino *2020-07-17 13:19:03*


###  [#82](https://github.com/bsorrentino/maven-annotation-plugin/issues/82) New v4.0 does not support Java 8    *bug*  *under investigation*  

**issue #82 - JDK8 compatibility**


[8117a6bb12cb71a](https://github.com/bsorrentino/maven-annotation-plugin/commit/8117a6bb12cb71a) bartolomeo sorrentino *2020-07-22 08:43:30*


## v4.0
### Generic changes

**update version**


[229f2f4298ce034](https://github.com/bsorrentino/maven-annotation-plugin/commit/229f2f4298ce034) bsorrentino *2020-07-18 21:18:25*

**set release version**

 * update docs
 * update changelog

[dd12853b3452707](https://github.com/bsorrentino/maven-annotation-plugin/commit/dd12853b3452707) bsorrentino *2020-07-18 21:10:38*

**move to developer version**


[9ad2634520c0855](https://github.com/bsorrentino/maven-annotation-plugin/commit/9ad2634520c0855) bartolomeo sorrentino *2020-07-17 16:47:17*

**Create FUNDING.yml**


[d0566025a1d36c9](https://github.com/bsorrentino/maven-annotation-plugin/commit/d0566025a1d36c9) bsorrentino *2020-05-27 09:17:44*


## v4.0-rc1
### Generic changes

**update readme**


[2262a4d28954925](https://github.com/bsorrentino/maven-annotation-plugin/commit/2262a4d28954925) bsorrentino *2020-04-17 16:16:12*

**update chagelog**


[d444f63f9c4bed9](https://github.com/bsorrentino/maven-annotation-plugin/commit/d444f63f9c4bed9) bartolomeo sorrentino *2020-04-17 15:40:13*

**move to next release version**


[4146d73e88ea389](https://github.com/bsorrentino/maven-annotation-plugin/commit/4146d73e88ea389) bartolomeo sorrentino *2020-04-17 15:37:40*

**update readme**


[807678003bfcd70](https://github.com/bsorrentino/maven-annotation-plugin/commit/807678003bfcd70) bartolomeo sorrentino *2020-04-16 18:39:07*

**update changelog template**


[8ae0d2f095d87b0](https://github.com/bsorrentino/maven-annotation-plugin/commit/8ae0d2f095d87b0) bartolomeo sorrentino *2020-03-20 09:22:18*

**update changelog**


[7e2cd9fb361848e](https://github.com/bsorrentino/maven-annotation-plugin/commit/7e2cd9fb361848e) bartolomeo sorrentino *2020-03-20 09:22:00*

**add utils javadoc to the site**


[2dda14ced574f7a](https://github.com/bsorrentino/maven-annotation-plugin/commit/2dda14ced574f7a) bartolomeo sorrentino *2020-03-02 21:50:12*

**update readme**


[bcfd9b3ecc46e6a](https://github.com/bsorrentino/maven-annotation-plugin/commit/bcfd9b3ecc46e6a) bsorrentino *2020-03-02 20:03:36*


## v4.0-beta1
### Generic changes

**remove test module**


[fb66eab913100ea](https://github.com/bsorrentino/maven-annotation-plugin/commit/fb66eab913100ea) bsorrentino *2020-03-02 19:56:29*

**prepare for release**


[167f62179553548](https://github.com/bsorrentino/maven-annotation-plugin/commit/167f62179553548) bartolomeo sorrentino *2020-03-02 19:39:55*

**remove netbeans references**


[04a8f939627a8ac](https://github.com/bsorrentino/maven-annotation-plugin/commit/04a8f939627a8ac) Bartolomeo Sorrentino *2019-04-22 17:00:51*

**update readme**


[2d639c43eb66e2a](https://github.com/bsorrentino/maven-annotation-plugin/commit/2d639c43eb66e2a) bsorrentino *2018-08-12 13:54:32*


## v3.3.3
### Generic changes

**update release**


[393a51d1639f1ea](https://github.com/bsorrentino/maven-annotation-plugin/commit/393a51d1639f1ea) bsorrentino *2018-02-24 11:45:59*

**merge hotfix**


[df019e60082b212](https://github.com/bsorrentino/maven-annotation-plugin/commit/df019e60082b212) bsorrentino *2017-09-12 09:09:09*

**merge hotfix**


[f1dde13e924cb73](https://github.com/bsorrentino/maven-annotation-plugin/commit/f1dde13e924cb73) bsorrentino *2017-09-12 09:07:36*

**update readme**


[f37985e048b01f1](https://github.com/bsorrentino/maven-annotation-plugin/commit/f37985e048b01f1) bsorrentino *2017-09-12 09:06:18*

**update doc**


[469b8c60cbb92c8](https://github.com/bsorrentino/maven-annotation-plugin/commit/469b8c60cbb92c8) bsorrentino *2017-09-07 11:44:17*

**update readme**


[00b4ca81a0472f4](https://github.com/bsorrentino/maven-annotation-plugin/commit/00b4ca81a0472f4) bsorrentino *2017-09-07 11:24:33*

**update readme**


[667baa6d69b44b0](https://github.com/bsorrentino/maven-annotation-plugin/commit/667baa6d69b44b0) bsorrentino *2017-09-07 11:23:25*

**update readme**


[a0d31294e3e7551](https://github.com/bsorrentino/maven-annotation-plugin/commit/a0d31294e3e7551) bsorrentino *2017-09-07 11:20:28*

**update to next version**


[1c2ff82d8877d45](https://github.com/bsorrentino/maven-annotation-plugin/commit/1c2ff82d8877d45) bsorrentino *2017-09-07 11:13:26*


###  [#72](https://github.com/bsorrentino/maven-annotation-plugin/issues/72) Multiple executions of plugin    *question*  

**Issue #72 - Add notes to documentation**


[babeeb619ce69ab](https://github.com/bsorrentino/maven-annotation-plugin/commit/babeeb619ce69ab) bsorrentino *2018-08-12 13:39:42*


###  [#75](https://github.com/bsorrentino/maven-annotation-plugin/issues/75) Add support for Java9 --release parameter    *enhancement*  

**add support for --relase option #75**


[9bd60c8b23aa980](https://github.com/bsorrentino/maven-annotation-plugin/commit/9bd60c8b23aa980) bsorrentino *2017-11-28 23:32:56*


## v3.3.2
### Generic changes

**update README**


[4619f9670511292](https://github.com/bsorrentino/maven-annotation-plugin/commit/4619f9670511292) bsorrentino *2017-09-07 10:52:30*

**prepare for release**


[7a6ee16de022056](https://github.com/bsorrentino/maven-annotation-plugin/commit/7a6ee16de022056) bsorrentino *2017-09-07 10:43:46*

**Windows path separator fix**


[d22ab3b8a0be5b3](https://github.com/bsorrentino/maven-annotation-plugin/commit/d22ab3b8a0be5b3) Christian Beikov *2017-09-07 10:25:59*

**Pass through additional compiler arguments**

 * This will allow to pass arguments like &quot;--add-modules=java.se.ee&quot; as `compilerArguments`

[fed8bfecc523ec9](https://github.com/bsorrentino/maven-annotation-plugin/commit/fed8bfecc523ec9) Christian Beikov *2017-09-07 10:06:58*

**update ignore**


[ef30ce5fdb71f82](https://github.com/bsorrentino/maven-annotation-plugin/commit/ef30ce5fdb71f82) bsorrentino *2017-07-30 16:11:50*

**merge from hotfix**


[a8d17f63fe747b5](https://github.com/bsorrentino/maven-annotation-plugin/commit/a8d17f63fe747b5) bsorrentino *2017-04-11 20:30:30*

**update test version**


[d5b95a9ac4845f6](https://github.com/bsorrentino/maven-annotation-plugin/commit/d5b95a9ac4845f6) bsorrentino *2017-04-11 20:29:06*

**update test version**


[276e977ec9dfc29](https://github.com/bsorrentino/maven-annotation-plugin/commit/276e977ec9dfc29) bsorrentino *2017-04-11 20:28:07*

**move to next version**


[9d9a5d185241e67](https://github.com/bsorrentino/maven-annotation-plugin/commit/9d9a5d185241e67) bsorrentino *2017-04-11 20:25:40*


###  [#68](https://github.com/bsorrentino/maven-annotation-plugin/issues/68) License inconsistency  

**#68 - update license tag**


[1e43ba3b13f4ccb](https://github.com/bsorrentino/maven-annotation-plugin/commit/1e43ba3b13f4ccb) bsorrentino *2017-07-30 16:10:49*


###  [#69](https://github.com/bsorrentino/maven-annotation-plugin/issues/69) Java 9 support    *enhancement*  

**fix #69 merge #70**

 * Merge branch &#39;release/3.3.2&#39;

[694b5232f4369d5](https://github.com/bsorrentino/maven-annotation-plugin/commit/694b5232f4369d5) bsorrentino *2017-09-07 11:07:24*

**#69 remove redundant if**


[4cefcc36056e9af](https://github.com/bsorrentino/maven-annotation-plugin/commit/4cefcc36056e9af) bsorrentino *2017-09-07 10:38:51*


###  [#70](https://github.com/bsorrentino/maven-annotation-plugin/pull/70) Pass through additional compiler arguments    *enhancement*  

**fix #69 merge #70**

 * Merge branch &#39;release/3.3.2&#39;

[694b5232f4369d5](https://github.com/bsorrentino/maven-annotation-plugin/commit/694b5232f4369d5) bsorrentino *2017-09-07 11:07:24*


## v3.3.1
### Generic changes

**prepare release**


[91113cb72b411ac](https://github.com/bsorrentino/maven-annotation-plugin/commit/91113cb72b411ac) bsorrentino *2017-04-11 20:16:30*

**move to next dev version**


[6709b3a8f23fc9f](https://github.com/bsorrentino/maven-annotation-plugin/commit/6709b3a8f23fc9f) bsorrentino *2017-04-10 17:38:10*

**add support of env vars : maven.processor.source & maven.processor.target**


[4e81968ea5ee538](https://github.com/bsorrentino/maven-annotation-plugin/commit/4e81968ea5ee538) bsorrentino *2017-04-09 11:10:32*

**finalize Toolchain integration**


[5dc726a14ca66cc](https://github.com/bsorrentino/maven-annotation-plugin/commit/5dc726a14ca66cc) bsorrentino *2017-04-09 10:58:55*

**add ToolchainManager component**


[0e6e2947d94ccbc](https://github.com/bsorrentino/maven-annotation-plugin/commit/0e6e2947d94ccbc) bsorrentino *2017-04-08 20:04:57*

**update**


[40a6e2ec2ab4686](https://github.com/bsorrentino/maven-annotation-plugin/commit/40a6e2ec2ab4686) bsorrentino *2017-03-28 16:14:31*

**Customize Plexus Compiler to capture output**


[8ce007e4f1f97d0](https://github.com/bsorrentino/maven-annotation-plugin/commit/8ce007e4f1f97d0) bsorrentino *2017-03-28 11:08:12*

**plexus compiler refinements**


[384cc666c61d4ce](https://github.com/bsorrentino/maven-annotation-plugin/commit/384cc666c61d4ce) bsorrentino *2017-03-27 22:45:50*

**add support of plexus compiler**


[91128bea35178d1](https://github.com/bsorrentino/maven-annotation-plugin/commit/91128bea35178d1) bsorrentino *2017-03-21 17:14:50*

**move to next develop version**


[75059592db5173e](https://github.com/bsorrentino/maven-annotation-plugin/commit/75059592db5173e) bsorrentino *2017-03-09 16:39:07*


###  [#66](https://github.com/bsorrentino/maven-annotation-plugin/issues/66) (use -source 8 or higher to enable lambda expressions)    *bug*  

**fix issue#66 and issue#67**


[c5dd497e8f2477a](https://github.com/bsorrentino/maven-annotation-plugin/commit/c5dd497e8f2477a) bsorrentino *2017-04-11 20:00:12*


###  [#67](https://github.com/bsorrentino/maven-annotation-plugin/issues/67) from version  3.3 options are not taking in consideration    *bug*  

**fix issue#66 and issue#67**


[c5dd497e8f2477a](https://github.com/bsorrentino/maven-annotation-plugin/commit/c5dd497e8f2477a) bsorrentino *2017-04-11 20:00:12*


## v3.3
### Generic changes

**update comments**


[063f735be3a4227](https://github.com/bsorrentino/maven-annotation-plugin/commit/063f735be3a4227) bsorrentino *2017-04-10 17:34:50*

**update readme**


[fa257b153e9cb95](https://github.com/bsorrentino/maven-annotation-plugin/commit/fa257b153e9cb95) bsorrentino *2017-04-10 13:20:19*

**update site doc**


[165ad0853b3ed37](https://github.com/bsorrentino/maven-annotation-plugin/commit/165ad0853b3ed37) bsorrentino *2017-04-10 13:18:45*

**update README**


[b36c0435ecb71e2](https://github.com/bsorrentino/maven-annotation-plugin/commit/b36c0435ecb71e2) bsorrentino *2017-04-09 17:59:47*

**update readme**


[83635f07abf09eb](https://github.com/bsorrentino/maven-annotation-plugin/commit/83635f07abf09eb) bsorrentino *2017-04-09 17:44:03*

**prepare for release**


[fc0f4631c9e0a08](https://github.com/bsorrentino/maven-annotation-plugin/commit/fc0f4631c9e0a08) bsorrentino *2017-04-09 17:33:55*

**update doc**


[eeb362efe21faa7](https://github.com/bsorrentino/maven-annotation-plugin/commit/eeb362efe21faa7) bsorrentino *2016-10-07 13:24:41*


## v3.2.0
### Generic changes

**update for release 3.2.0**


[c144aec79429c54](https://github.com/bsorrentino/maven-annotation-plugin/commit/c144aec79429c54) bsorrentino *2016-10-07 13:07:59*

**get sourcepath from project.getCompileSourceRoot()**


[29deb573c93a757](https://github.com/bsorrentino/maven-annotation-plugin/commit/29deb573c93a757) bsorrentino *2016-09-28 11:37:34*

**update projects description**


[0b6bc2c37173a44](https://github.com/bsorrentino/maven-annotation-plugin/commit/0b6bc2c37173a44) bsorrentino *2016-09-12 14:57:20*

**add utils and test project**


[30bbb057c63be23](https://github.com/bsorrentino/maven-annotation-plugin/commit/30bbb057c63be23) bsorrentino *2016-09-12 14:43:45*

**add -sourcepath option**


[94f1fe0ff5aa55e](https://github.com/bsorrentino/maven-annotation-plugin/commit/94f1fe0ff5aa55e) bsorrentino *2016-09-12 14:30:30*

**update links**


[7b10c05f908a8a4](https://github.com/bsorrentino/maven-annotation-plugin/commit/7b10c05f908a8a4) bsorrentino *2016-02-02 22:30:10*

**update to next development release**


[eee1a25b33dc0c3](https://github.com/bsorrentino/maven-annotation-plugin/commit/eee1a25b33dc0c3) bsorrentino *2016-02-02 22:28:00*


## v3.1.0
### Generic changes

**update README**


[b0f2f4fd56a3264](https://github.com/bsorrentino/maven-annotation-plugin/commit/b0f2f4fd56a3264) bsorrentino *2016-02-02 22:24:48*

**Add "skip" property to MOJOs**

 * This fixes https://github.com/bsorrentino/maven-annotation-plugin/issues/59

[c674eaa8be96a44](https://github.com/bsorrentino/maven-annotation-plugin/commit/c674eaa8be96a44) Boris Brodski *2016-01-28 17:50:04*

**update doc**


[41973e17f79b1fd](https://github.com/bsorrentino/maven-annotation-plugin/commit/41973e17f79b1fd) bsorrentino *2015-04-07 16:18:50*

**update issues link**


[d6b9599560fc01e](https://github.com/bsorrentino/maven-annotation-plugin/commit/d6b9599560fc01e) bsorrentino *2015-04-07 16:17:24*

**update site**


[215d2050a509f44](https://github.com/bsorrentino/maven-annotation-plugin/commit/215d2050a509f44) bsorrentino *2015-03-19 20:35:37*

**update doc**


[3a301b758d984ac](https://github.com/bsorrentino/maven-annotation-plugin/commit/3a301b758d984ac) bsorrentino *2015-03-19 20:31:19*

**Create README.md**


[b8a9ccfd2c97357](https://github.com/bsorrentino/maven-annotation-plugin/commit/b8a9ccfd2c97357) bsorrentino *2015-03-18 14:21:44*

**update site skin**


[fe5256ee0da3045](https://github.com/bsorrentino/maven-annotation-plugin/commit/fe5256ee0da3045) bsorrentino *2014-06-28 21:05:37*


###  [#61](https://github.com/bsorrentino/maven-annotation-plugin/pull/61) Add &quot;skip&quot; property to MOJOs  

**pull request #61 merged**

 * site deploy on branch gh-pages automated
 * site plugin updated

[05e9e0e92cb38ee](https://github.com/bsorrentino/maven-annotation-plugin/commit/05e9e0e92cb38ee) bsorrentino *2016-02-02 21:57:32*


## maven-processor-plugin-3.1.0-beta1
### Generic changes

**update compiler plugin version**


[f1b29c955fe99be](https://github.com/bsorrentino/maven-annotation-plugin/commit/f1b29c955fe99be) bsorrentino *2014-06-28 16:54:08*

**fix issue 56**


[b0b4a24b15a5cff](https://github.com/bsorrentino/maven-annotation-plugin/commit/b0b4a24b15a5cff) bsorrentino *2014-06-28 16:39:52*

**fix problem on windows os**


[35541bcd173d4c0](https://github.com/bsorrentino/maven-annotation-plugin/commit/35541bcd173d4c0) bsorrentino *2013-09-18 13:00:14*

**update error message**


[3746795747919e0](https://github.com/bsorrentino/maven-annotation-plugin/commit/3746795747919e0) bsorrentino *2013-09-17 09:49:16*

**require maven 3.1**


[65188be477a8ca2](https://github.com/bsorrentino/maven-annotation-plugin/commit/65188be477a8ca2) bsorrentino *2013-09-15 20:52:29*

**issue55 plugin for maven release 3.1.0**


[79bd3e63fe9b3af](https://github.com/bsorrentino/maven-annotation-plugin/commit/79bd3e63fe9b3af) bsorrentino *2013-09-15 20:48:34*

**issue55 plugin for maven release 3.0.5**


[0a2400736eccf2e](https://github.com/bsorrentino/maven-annotation-plugin/commit/0a2400736eccf2e) bsorrentino *2013-09-15 20:28:42*

**issue55**


[6106c78b7de5e53](https://github.com/bsorrentino/maven-annotation-plugin/commit/6106c78b7de5e53) bsorrentino *2013-09-15 19:20:37*


## maven-processor-plugin-2.2.4
### Generic changes

**Issue 54**


[e92be425742664f](https://github.com/bsorrentino/maven-annotation-plugin/commit/e92be425742664f) softphone *2013-06-14 19:44:13*


## maven-processor-plugin-2.2.3
### Generic changes

**Issue 53**


[60db10784d6b596](https://github.com/bsorrentino/maven-annotation-plugin/commit/60db10784d6b596) softphone *2013-05-22 20:53:02*


## maven-processor-plugin-2.2.2
### Generic changes

**Issue 48**


[70957ebf1386ce3](https://github.com/bsorrentino/maven-annotation-plugin/commit/70957ebf1386ce3) softphone *2013-05-14 13:28:18*


## maven-processor-plugin-2.2.1
### Generic changes

**Issue 51**


[bbfd5ea26f874c0](https://github.com/bsorrentino/maven-annotation-plugin/commit/bbfd5ea26f874c0) softphone *2013-04-06 12:34:06*


## maven-processor-plugin-2.2.0
### Generic changes

**merge patch from Heiko Braun**


[c7f9172bc143a11](https://github.com/bsorrentino/maven-annotation-plugin/commit/c7f9172bc143a11) bsorrentino *2013-04-03 15:32:13*


## maven-processor-plugin-2.1.1
### Generic changes

**issue 47**


[68d6174fd75a59d](https://github.com/bsorrentino/maven-annotation-plugin/commit/68d6174fd75a59d) softphone *2013-01-30 13:43:39*

**update unit test**


[e29da4cf58db458](https://github.com/bsorrentino/maven-annotation-plugin/commit/e29da4cf58db458) softphone *2013-01-26 21:19:00*


## maven-processor-plugin-2.1.0
### Generic changes

**issue46**


[20a4b6ad38e80f8](https://github.com/bsorrentino/maven-annotation-plugin/commit/20a4b6ad38e80f8) softphone *2012-11-01 13:50:49*

**allow maven3 report generation**


[64b0901fbc675e2](https://github.com/bsorrentino/maven-annotation-plugin/commit/64b0901fbc675e2) softphone *2012-10-17 21:32:51*


## maven-processor-plugin-2.1.0-beta1
### Generic changes

**update docs url**


[77f6a994384d49d](https://github.com/bsorrentino/maven-annotation-plugin/commit/77f6a994384d49d) softphone *2012-10-17 20:23:32*

**organize import**


[9309c89f4d2bfa8](https://github.com/bsorrentino/maven-annotation-plugin/commit/9309c89f4d2bfa8) softphone *2012-10-17 18:51:21*

**Issue 44**


[57a0baf1a1cc8b0](https://github.com/bsorrentino/maven-annotation-plugin/commit/57a0baf1a1cc8b0) bsorrentino *2012-10-12 16:02:24*


## maven-processor-plugin-2.0.8
### Generic changes

**update release**


[e7a28e644424dc5](https://github.com/bsorrentino/maven-annotation-plugin/commit/e7a28e644424dc5) bsorrentino *2012-10-09 09:05:32*

**Issue 43**


[d5ca7ea13f28c38](https://github.com/bsorrentino/maven-annotation-plugin/commit/d5ca7ea13f28c38) bsorrentino *2012-10-08 15:14:37*


## maven-processor-plugin-2.0.7
### Generic changes

**revert to 7c9b55a41816**


[0ed5a71475e76d4](https://github.com/bsorrentino/maven-annotation-plugin/commit/0ed5a71475e76d4) bsorrentino *2012-10-09 08:13:17*

**Issue 42**


[7c9b55a41816270](https://github.com/bsorrentino/maven-annotation-plugin/commit/7c9b55a41816270) bsorrentino *2012-08-27 14:47:44*

**Issue 43**


[34ac342d30de616](https://github.com/bsorrentino/maven-annotation-plugin/commit/34ac342d30de616) softphone *2012-08-26 18:41:20*

**Issue 42 apply patch**


[5f82c3d82f3d3c9](https://github.com/bsorrentino/maven-annotation-plugin/commit/5f82c3d82f3d3c9) bsorrentino *2012-08-26 17:21:54*


## maven-processor-plugin-2.0.6
### Generic changes

**update scm to git**


[54d09d93cad49e8](https://github.com/bsorrentino/maven-annotation-plugin/commit/54d09d93cad49e8) bsorrentino *2012-08-07 08:23:05*

**update**


[4c7b75962c4446b](https://github.com/bsorrentino/maven-annotation-plugin/commit/4c7b75962c4446b) bsorrentino *2012-08-07 08:16:47*

**update ignore**


[a480a4273587a61](https://github.com/bsorrentino/maven-annotation-plugin/commit/a480a4273587a61) bsorrentino *2012-08-07 08:13:53*

**sync refinements**


[bf958dd87dd0dcd](https://github.com/bsorrentino/maven-annotation-plugin/commit/bf958dd87dd0dcd) bsorrentino *2012-06-26 07:56:40*

**first import**


[fe72619e8ba7d55](https://github.com/bsorrentino/maven-annotation-plugin/commit/fe72619e8ba7d55) bsorrentino *2012-06-25 20:29:30*

**initial import**


[a6874bc1ff14c88](https://github.com/bsorrentino/maven-annotation-plugin/commit/a6874bc1ff14c88) bsorrentino *2012-06-25 16:48:43*

**update**


[7947063192fb47f](https://github.com/bsorrentino/maven-annotation-plugin/commit/7947063192fb47f) bsorrentino *2012-06-25 16:44:59*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@23 c416075f-80b4-e980-4839-00ea3ed24e77**


[55f7bad93e6f969](https://github.com/bsorrentino/maven-annotation-plugin/commit/55f7bad93e6f969) valery.isaev@gmail.com *2011-05-30 22:19:40*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@22 c416075f-80b4-e980-4839-00ea3ed24e77**


[95968c267a723a9](https://github.com/bsorrentino/maven-annotation-plugin/commit/95968c267a723a9) valery.isaev@gmail.com *2011-05-30 19:34:39*

**autotools**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@21 c416075f-80b4-e980-4839-00ea3ed24e77

[b81461aaf2af6b6](https://github.com/bsorrentino/maven-annotation-plugin/commit/b81461aaf2af6b6) valery.isaev@gmail.com *2011-05-30 13:28:43*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@20 c416075f-80b4-e980-4839-00ea3ed24e77**


[df3bfd087410566](https://github.com/bsorrentino/maven-annotation-plugin/commit/df3bfd087410566) valery.isaev@gmail.com *2011-05-29 13:07:53*

**config**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@19 c416075f-80b4-e980-4839-00ea3ed24e77

[2a0f098cf259a56](https://github.com/bsorrentino/maven-annotation-plugin/commit/2a0f098cf259a56) valery.isaev@gmail.com *2011-05-27 21:57:33*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@18 c416075f-80b4-e980-4839-00ea3ed24e77**


[bffbbceebf2f845](https://github.com/bsorrentino/maven-annotation-plugin/commit/bffbbceebf2f845) valery.isaev@gmail.com *2011-04-25 11:23:57*

**magic added**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@17 c416075f-80b4-e980-4839-00ea3ed24e77

[7db308b4bc8d4f2](https://github.com/bsorrentino/maven-annotation-plugin/commit/7db308b4bc8d4f2) valery.isaev@gmail.com *2011-03-28 13:19:58*

**minor fixes**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@16 c416075f-80b4-e980-4839-00ea3ed24e77

[9a616dc849b8a73](https://github.com/bsorrentino/maven-annotation-plugin/commit/9a616dc849b8a73) valery.isaev@gmail.com *2011-03-28 00:04:58*

**image comparison**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@15 c416075f-80b4-e980-4839-00ea3ed24e77

[ac33873072edf71](https://github.com/bsorrentino/maven-annotation-plugin/commit/ac33873072edf71) valery.isaev@gmail.com *2011-03-27 22:33:28*

**precompare**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@14 c416075f-80b4-e980-4839-00ea3ed24e77

[ab43a43c581bdfc](https://github.com/bsorrentino/maven-annotation-plugin/commit/ab43a43c581bdfc) valery.isaev@gmail.com *2011-03-27 18:46:05*

**missing files added**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@13 c416075f-80b4-e980-4839-00ea3ed24e77

[a0c5f27a0f67c1f](https://github.com/bsorrentino/maven-annotation-plugin/commit/a0c5f27a0f67c1f) valery.isaev@gmail.com *2011-03-23 19:32:10*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@12 c416075f-80b4-e980-4839-00ea3ed24e77**


[5b40a56e28847de](https://github.com/bsorrentino/maven-annotation-plugin/commit/5b40a56e28847de) valery.isaev@gmail.com *2011-03-23 18:39:30*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@11 c416075f-80b4-e980-4839-00ea3ed24e77**


[ae9b7905bf47ac5](https://github.com/bsorrentino/maven-annotation-plugin/commit/ae9b7905bf47ac5) valery.isaev@gmail.com *2011-03-23 08:17:42*

**grouping comparator added**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@10 c416075f-80b4-e980-4839-00ea3ed24e77

[e752bc478c1bbff](https://github.com/bsorrentino/maven-annotation-plugin/commit/e752bc478c1bbff) valery.isaev@gmail.com *2011-03-22 21:26:59*

**clusterization added**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@9 c416075f-80b4-e980-4839-00ea3ed24e77

[a397a365bb84d5f](https://github.com/bsorrentino/maven-annotation-plugin/commit/a397a365bb84d5f) valery.isaev@gmail.com *2011-03-21 21:07:17*

**error handling added**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@8 c416075f-80b4-e980-4839-00ea3ed24e77

[87d1e30973e4751](https://github.com/bsorrentino/maven-annotation-plugin/commit/87d1e30973e4751) valery.isaev@gmail.com *2011-03-21 19:26:00*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@7 c416075f-80b4-e980-4839-00ea3ed24e77**


[9ad65ebfcff060b](https://github.com/bsorrentino/maven-annotation-plugin/commit/9ad65ebfcff060b) valery.isaev@gmail.com *2011-03-21 17:14:29*

**add file types**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@6 c416075f-80b4-e980-4839-00ea3ed24e77

[26178ed3ba6920b](https://github.com/bsorrentino/maven-annotation-plugin/commit/26178ed3ba6920b) valery.isaev@gmail.com *2011-03-16 17:33:52*

**added forgotten files**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@5 c416075f-80b4-e980-4839-00ea3ed24e77

[ec42fe6a4f5c3ea](https://github.com/bsorrentino/maven-annotation-plugin/commit/ec42fe6a4f5c3ea) valery.isaev@gmail.com *2011-03-15 17:55:23*

**git-svn-id: https://projectname.googlecode.com/svn/trunk@4 c416075f-80b4-e980-4839-00ea3ed24e77**


[c5991caa924b465](https://github.com/bsorrentino/maven-annotation-plugin/commit/c5991caa924b465) valery.isaev@gmail.com *2011-03-15 17:54:25*

**some makefile improvements**

 * added sequences
 * git-svn-id: https://projectname.googlecode.com/svn/trunk@3 c416075f-80b4-e980-4839-00ea3ed24e77

[4b6a2bd4275193b](https://github.com/bsorrentino/maven-annotation-plugin/commit/4b6a2bd4275193b) valery.isaev@gmail.com *2011-03-14 11:09:56*

**first commit**

 * git-svn-id: https://projectname.googlecode.com/svn/trunk@2 c416075f-80b4-e980-4839-00ea3ed24e77

[22a3c1b1a9be1a6](https://github.com/bsorrentino/maven-annotation-plugin/commit/22a3c1b1a9be1a6) valery.isaev@gmail.com *2011-03-13 00:01:25*


