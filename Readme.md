javaee-maven-parent
====================

Parent POM for JavaEE7 based projects. Provides default project build configuration.


Introduction
---------------------

The Java Maven parent POM provides default configuration for JavaEE7 based Maven applications.

* Based on [java-maven-parent](https://github.com/MSzturc/java-maven-parent)
* Provides a testing stack based on arquillian including the following modules:
  * shrinkwrap
  * drone
  * graphene
  * selenium
* Includes Maven Profiles for embedded testing of managed javaee application on the following application servers:
  * Glassfish 3.1.2.2
  * Glassfish 4.0
  * Glassfish 4.1
  * TomEE 1.7.1
  * Wildfly 8.0
  * Wildfly 8.1
  * Wildfly 8.2


Usage
---------------------

Start out by adding the parent configuration to your pom.
	
    <parent>
        <groupId>de.mszturc</groupId>
        <artifactId>javaee-parent</artifactId>
        <version>1.0</version>
    </parent>

The pom includes properties which allow various build configuration to be 
customized.  For example, to override the default version of the
maven-compiler-plugin, just set a property.

    <properties>
      <maven.compiler.plugin.version>3.3</maven.compiler.plugin.version>
    </properties>

Or override the default Java compiler source and target level used in the build.  
Note the default level is 1.8.

    <properties>
      <project.build.sourceLevel>1.7</project.build.sourceLevel>
      <project.build.targetLevel>1.7</project.build.targetLevel>
    </properties>

	
The Glassfish Profiles
--------------------
The parent POM includes a Maven profiles called "glassfish-X.X". This profile runs the managed assemblies on an embedded Glassfish Application Server.
When used the defined plugins will run and connect to a embedded(same JVM) GlassFish instance. This implementation has lifecycle support, so the container will be started and stopped as part of the test run.

A default data source, jdbc/__default, is configured using the embedded Derby database for testing purpose.


To trigger a wildfly based test from the CLI use the following command:

    mvn -Pglassfish-X.X
	
	
The TomEE Profile
--------------------
The parent POM includes a Maven profiles called "tomee-1.7.1". This profile runs the managed assemblies on an embedded TomEE Application Server.
When used the defined plugins will handle the business of starting/stopping servers, build/deploying war files and finally running your tests.


To trigger a wildfly based test from the CLI use the following command:

    mvn -Ptomee-1.7.1
	
The Wildfly Profiles
--------------------
The parent POM includes a Maven profiles called "wildfly-8.X-final". This profile runs the managed assemblies on an embedded JBoss Wildfly Application Server.
When used the defined plugins will perform the following:

* Download and unzip under the /target directory a fresh copy of Wildly 8.X, that will be used as a managed-container to run the tests.
* Configure the maven-surefire plugin to the above directory.

A default data source, ExampleDS, is configured using the embedded H2 database for testing purpose.


To trigger a wildfly based test from the CLI use the following command:

    mvn -Pwildfly-8.X-final
	
	
Technical Notes
---------------------

For the creation of the project I used the following tools & plugins:

- Java JDK 1.8.0_25-b18 x64
- Maven 3.1.1

The project was test in the following environment:

- Windows 7 x64
- Java JDK 1.8.0_25-b18 x64
- Maven 3.1.1

On following Application Servers:

- Glassfish 3.1.2.2
- Glassfish 4.0
- Glassfish 4.1
- TomEE 1.7.1
- Wildfly 8.0
- Wildfly 8.1
- Wildfly 8.2