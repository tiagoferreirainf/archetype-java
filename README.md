# Archetypes in java

Example of an archetype with a multi maven project constituted by a springboot application, docker conteinerization of 
the microservice and the respective helmchart.

Archetype can be found in this [folder.](./springdockerhelm) 


## How to Create an archetype
### Simple module archetype
Start by creating a generic maven project with a _pom.xml_ file 
and a the traditional folder structure, that will be used as the new project template.

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

First, it is necessary to create the new maven project structure under the folder _archetypes-resources_, 
basically we create a "complete" maven project inside it and a _archetype-metadata.xml_ file in the _META-INF/maven/_ folder as follows:

````
project
| src
| | main
| | | java
| | | resources
| | | archetype-resources           <- new folder 
| | | | src
| | | | | pom.xml
| | | | | main
| | | | | | java
| | | | | | | mainclass.java
| | | | | test
| | | | | | java
| | | | | | | maintestclass.java
| | | META-INF                      <- new folder 
| | | | maven
| | | | | archetype-metadata.xml
| pom.xml
````

The _archetype-metadata.xml_ file will contain the instructions for the maven plugin to build the archetype.

Between this information, there is the defined set of files to be used by the archetype, but also the required set of properties that we want to configure.
Official documentation can be found [here.](https://maven.apache.org/archetype/maven-archetype-plugin/specification/archetype-metadata.html) 

Example, if we require a variable in a pom file like the java version in our template project:
````
<properties>
    <maven.compiler.source>${javaVersion}</maven.compiler.source>
    <maven.compiler.target>${javaVersion}</maven.compiler.target>
</properties>
````

The following must be added to the _archetype-metadata.xml_.
````
<requiredProperties>
    <requiredProperty key="javaVersion">
        <defaultValue>11</defaultValue>
    </requiredProperty>
</requiredProperties>
````

Full example can be seen in [template pom file.](./simpleproject/src/main/resources/archetype-resources/pom.xml) and [archetype-metadata.xml file.](./simpleproject/src/main/resources/META-INF/maven/archetype-metadata.xml)

Concluded this steps we just need to build the project and that's it

### Multi module archetype

A multimodule project is quite similar to the simple project the main diference being that each module is described individually in the [archetype-metadata.xml file.](./multiproject/src/main/resources/META-INF/maven/archetype-metadata.xml)

##Generate a maven project using the archetype
````
mvn archetype:generate -DarchetypeGroupId=ARCHETYPE_GROUP_ID \
    -DarchetypeArtifactId=ARCHETYPE_ARTIFACT_ID \
    -DarchetypeVersion=ARCHETYPE_VERSION \
    -DgroupId=NEW_PROJECT_GROUP_ID \
    -DartifactId=NEW_PROJECT_ARTIFACT_ID \
    -DCUSTOM_PROPS_KEY=CUSTOM_PROPS_VALUES
````