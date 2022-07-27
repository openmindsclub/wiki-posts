# Using Maven?

## Description

Maven is a project manager for Java projects providing tools for dependency management, building, packaging and all kind of other project life cycles.

## Prerequirement

* Basic knowledge on `xml` file format.  
* A JDK (from version `1.7` and above)
* Install maven and add it to `PATH` variable (obviously) https://maven.apache.org/download.cgi 

## Setup maven on a Java project
### ⭐ (Beginner)
**reference:** https://maven.apache.org/guides/introduction/introduction-to-the-pom.html

On the root directory of your Java project, create a `pom.xml` file, POM stands for Project Object Model.
This file will hold our Maven's configuration file for the current project, now add the following content:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>your.package.name</groupId>
  <artifactId>ArtifactName</artifactId>
  <packaging>jar</packaging> 
  
  <name>ProjectName</name>
  <description>Project description</description>
  <version>1.0</version>
</project>
```
As you may already notice, our project configuration is inside 
`<project>` tag, the most important options indside it are:
* `modelVersion`: The `pom.xml` file version, always set it to `4.0.0`.
* `groupid`: Simply your package name example: `me.abdera7mane`, `com.google` (it's your domain name reversed all lower case).
* `packaging` The type of packaging, default to `jar`, this is the output file format after building.
* `name`: Project's name.
* `description`: Project's description.
* `version`: Project's version.

## Add properties
### ⭐ (Beginner)
**reference:** https://maven.apache.org/guides/introduction/introduction-to-the-pom.html#available-variables

Think of properties as creating variables inside `pom.xml`, here is an example:
```xml
<!-- Inside <project> tag -->
<properties>
  <java.version>11</java.version>
</properties>
```
in that example I created a variable named `java.version` with a value of `11`
how to use that variable you may ask ? simple write `${java.version}`
and maven will automatically replace all the occurrences with their  value when it reads the file.
 
## Configure Building
### ⭐⭐ (Pre-Intermediate)
**reference:** https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

So far, our `pom.xml` does nothing special, it is useless, so let's give it a goal ! We will tell maven how we want our project to be built:
```xml
<!-- Inside <project> tag -->
 <build>
  <defaultGoal>clean package</defaultGoal>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.7.0</version>
      <configuration>
        <source>${java.version}</source>
        <target>${java.version}</target>
      </configuration>
    </plugin>
  </plugins>
</build>
```

Wow there is so much going on ! don't worry it's not that complicated, let us go through the config node by node.
We first added a `build` tag, all the build configuration goes there, 
next we added `plugins` tag, yes maven is extensible ! and then  we added a plugin using `plugin` tag, now here are the basic settings to import plugins in maven:
* `groupId`: The package name of the plugin.
* `artifactId`: The plugin's name.
* `version`: Plugin's version.
* `configuration`: this varies from plugin to an other, you better check the plugin's documention for more detail on how to configure it.
In this example we are using `maven-compiler-plugin` which will help us compile and package our Java project to a jar file,
we only need to provide 2 config keys inside `configuration`:
    * `source`: The java language level used in the project.
    *  `target`: The java version used to compile the project.

now let's talk about `defaultGoal`, each plugin will execute based on a goal
in our case `clean package` (in other words after executing `mvn clean package` command)
specifying a `defaultGoal` will assign that goal to all active plugins and once that goal is called each plugin will trigger its functionality.

now to build the project just execute `mvn clean package`, the output should be generated in `target` directory.
 
## Importing dependencies
### ⭐⭐⭐ (Intermediate)
**reference:** https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html

Now this is the best feature I like on maven, you can import any library/dependency as long as it is hosted on a maven repository.
here is an example on installing `org.jetbrains.annotations` from https://mvnrepository.com/artifact/org.jetbrains/annotations:
```xml
<!-- Inside <project> tag -->
<dependencies>
  <dependency>
    <groupId>org.jetbrains</groupId>
    <artifactId>annotations</artifactId>
    <version>23.0.0</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```
You can already tell that all of our dependencies are defined inside `dependencies` tag and each `dependency` has its settings:
* `groupId`: Dependency's package name.
* `artifactId`: Dependency's name.
* `version`: Dependency version.
* `scope`: This can be 6 diffrent values:
  * `compile`: (default) Compile the dependency and include it in the final jar.
  * `provided`: Desn't include the dependency in the final jar, this is useful when you know that the dependency is included at runtime.
  * `test`: Only available to unit tests.
  * `system`: (*refer to the reference link*).
• `import`: not sure wth is this lol but in my experience it is very rarely used (*refer to the reference link*).

### ⚠️ Important Note

the dependency must be hosted on maven central repository which is at https://mvnrepository.com/,
if the dependency you want to install is somewhere else then you have to tell maven about the repository (also applies on maven plugins)
here is an example:
```xml 
<!-- Inside <project> tag -->
<repositories>
  <repository>
    <id>papermc</id>
    <url>https://papermc.io/repo/repository/maven-public/</url>
    <!-- Now maven knows where to look for com.destroystokyo.paper.paper-api -->
  </repository>
<repositories>

<dependencies>
  <dependency>
    <!-- Lives on https://papermc.io/repo/repository/maven-public/ -->
    <groupId>com.destroystokyo.paper</groupId>
    <artifactId>paper-api</artifactId>
    <version>1.16.5-R0.1-SNAPSHOT</version>
    <scope>provided</scope>
  </dependency>

  <dependency>
    <groupId>org.jetbrains</groupId>
    <artifactId>annotations</artifactId>
    <version>16.0.1</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```
This time I wanted to import `com.destroystokyo.paper.paper-api` as a dependency but it is hosted on https://papermc.io/repo/repository/maven-public/
We just had to add a repositories tag and then added a new repository setting:
* `id`: just an identifier to the repository.
* `url`: URL address to the repository.

yes this is very similar to `git add remote`

Now to download dependencies to your local machine simply run `mvn dependency:copy-dependencies`
maven will download them as jar files, if you want the source code instead add `-Dclassifier=sources` at the end of command,
they should be installed in `target/dependencies` directory
you can set a different output path by adding this argument `-DoutputDirectory="path/to/dir"` at the end of the command.

## Extra

Your IDE may already support maven by default, like `IntelliJ` which will auto detect `pom.xml`, it's preferable if you use maven from your IDE interface in that case
you don't have to install maven or worry about doing most of the configuration of `pom.xml`.
