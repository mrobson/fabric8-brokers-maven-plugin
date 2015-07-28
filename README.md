Exploring advanced features with the fabric8-maven-plugin
=========================================================
Author: Matt Robson

Technologies: Fuse, Fabric8, ActiveMQ, fabric8-maven-plugin, Profiles

Product: Fuse 6.1, ActiveMQ 6.1

Breakdown                                                                                                                     
---------                                                                                                                     
This is a command and profile based example to demonstrate the capabilities of the fabric8-maven-plugin.  We explore how to structure and maven project, creating ZIPs of our profiles in maven and how to commit those profiles into GIT through the build process.

For more information see:

* <https://access.redhat.com/site/documentation/JBoss_Fuse/> for more information about Red Hat JBoss Fuse
* <http://www.jboss.org/products/fuse/overview/> for more information about the upstream community
* <http://fabric8.io/> for more information about fabric8

System Requirements
-------------------
Before building out your Fabric, you will need:
* Java 1.7
* JBoss Fuse 6.1
* JBoss ActiveMQ 6.1

Prerequisites
-------------
* A working Fabric as outlined in part 1, 'fuse-fabric8-getting-started' <https://github.com/mrobson/fuse-fabric8-getting-started>

The Build Out                                                                                                             
-------------

1) clone the project

        git clone https://github.com/mrobson/fabric8-brokers-maven-plugin.git

2) change to project directory

        cd fabric8-brokers-maven-plugin

3) build the projects - this will create all of the profiles, their individual zips as well as an aggregate zip in 'fabric-aggregated-zip'

	mvn clean install

4) change to to source control build directory

	cd fabric-source-control-build

5) edit the git url for your purposes - either commit directly to fabric or to an internal maven repository

	vi pom.xml

	<configuration>
		<branchName>1.1</branchName>
		<!-- Branch to a known GIT repository outside Fuse -->
		<!--gitUrl>git@localhost.localdomain:prod/fabric8-git.git</gitUrl-->
		<!-- Branch to the GIT repository in Fuse -->
		<gitUrl>http://admin:admin@mrobson:8181/git/fabric</gitUrl>
		<oldBranchName>1.0</oldBranchName>
		<pushOnSuccess>true</pushOnSuccess>
	</configuration>

All fabric instances start at branch 1.0 (not master)!  So oldBranchName for a new fabric would be 1.0 with the branchName for the new branch being 1.1.  This will clone 1.0 and create a new branch 1.1 with the changes.  In fabric, wil will see a new version, 1.1 corresponding to the new branch.

Done!
	
	
	
	cd
This will deploy all 4 profiles.

	fabric-broker-base-profile
	fabric-redhat-broker1-profile
	fabric-redhat-broker2-profile
	fabric-redhat-broker-client-profile

