# Archetypes in java

## Goal
To create an archetype that can be used to create maven projects using the _maven-archetype-plugin_.

Two archetypes are going to be created, a simple module archetype and 
multi module maven projects.

This page explains how to:
- create base project
- generate archetype from project
- use generated archetype

## Create an Archetype

Start by creating a generic maven project, with a _pom.xml_ file and a the traditional folder structure.

````
project
| src
| | main
| | | java
| | | resources
| pom.xml
````

The _pom.xml_ should contain the archetype information and add to its content the _mave-archetype-plugin_.

````
<packaging>maven-archetype</packaging>

<build>
    <extensions>
        <extension>
            <groupId>org.apache.maven.archetype</groupId>
            <artifactId>archetype-packaging</artifactId>
            <version>3.2.1</version>
        </extension>
    </extensions>
</build>
````

Full example can be seen in [simpleproject pom file.](./simpleproject/pom.xml)

Concluding this, it's now time to create the archetype it self.

First, it is necessary to create the new maven project structure under the folder _archetypes-resources_, basically we create a "complete" maven project inside it as follows:

````
project
| src
| | main
| | | java
| | | resources
| | | archetype-resources     <- new folder 
| | | | src
| | | | | pom.xml
| | | | | main
| | | | | | java
| | | | | | | mainclass.java
| | | | | test
| | | | | | java
| | | | | | | maintestclass.java
| pom.xml
````

## Simple module archetype

## Multi module archetype

