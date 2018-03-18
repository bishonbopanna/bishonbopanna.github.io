---
layout: post
title:  "Hello World Spring-boot Web App"
date:   2018-03-14
categories: technology java spring-boot
permalink: /:categories/:title
---

This post is to understand what it takes to build a simple hello world spring-boot web app.

#### Requirement : Build simple Hello World spring-boot web app

#### Pre-requisites : 
-   Java 8 - Basic knowledge of Java programming language
-   Intellij Editor (If you dont have one you can download the community version from [here](https://www.jetbrains.com/idea/download){:target="_blank"})
-   Gradle (If you dont have gradle refer [here](https://gradle.org/install/){:target="_blank"}. On Mac I recommend to use "brew" to install gradle)
<br><br>

__Note : I am building this on Mac, if you are on different platform then you might have to map the commands to your platform specific ones__

_Understanding the requirements:_
    
#### What is a webapp or web application ?         
```
Web App or a web Application is an application that can be accessed over internet or intranet 
and allows users to perform actions. 
Example - Google Analytics, gmail, and jslint are web applications.  
```    
<br>
    
#### How is a website different from a web app ?                     
```
Websites are in general informational and not a whole lot of user interactions. Click on few 
buttons and they serve you some standard content.
Web apps on the other hand takes a user input and responds back with that particular user's response.
Example - 
    Website : News or weather information websites like cnn.com, weather.com
    Webapp  : Email app like gmail, when a user signs in, that user's emails are shown.
```
<br>
 
#### What is gradle ?                     
```
From Wiki: Gradle is an open-source build automation system that builds upon the concepts of 
Apache Ant and Apache Maven and introduces a Groovy-based domain-specific language (DSL) instead 
of the XML form used by Apache Maven for declaring the project configuration.
```
<br>

#### Is gradle/maven better than ant ?                    
```
Google will offer you n number of sites with detailed answer on this. 
But IMO what ant + ivy can do, gradle or maven alone can. 

If you did not undestand the previous statement, here is more eloborate answer:

Ant is a build tool mainly for java based apps, by itself it cannot manage your project
dependencies - all the jars that are needed to build your java based web app. You will
have to download specific versions of the jars and add them to a library and use it in 
your compile path of the web app. This becomes a major pain when you have to upgrade and
when the project size grows extensively like in enterprise app. Ant with Ivy can acheive
this, but you would still end up maintaining your jars in Ivy explicitly.

Maven and Gradle to the rescue - In the history of build tools,if ant is the gradfather,
then maven is the father and gradle is the son. That said, both maven and gradle solves the above.
In both these all you will have to do is specify the jar and its version in their respective
build configuration file - POM.xml (Project Object Model) for maven and build.gradle for gradle
and when you build all the jars are downloaded from maven central repository/website to your local.  
```

<br>
        
Now that we are better equipped about the requirement let us consider how we can achieve it.

With the intent of not recreating the wheel - [Here](https://spring.io/guides/gs/spring-boot/){:target="_blank"} 
is a great springio link we can refer to but approach it slightly differently

1.  Launch Intellij and create a project. Following screen shots should help :
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-1.png" width="450" height="400" alt="">
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-2.png" width="450" height="400" alt="">
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-3.png" width="450" height="400" alt="">
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-4.png" width="450" height="400" alt="">
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-5.png" width="450" height="400" alt="">
<br>

2.  Create a package inside the src/main/java/ :
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-6.png" width="500" height="250" alt="">
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-7.png" width="225" height="75" alt="">
<br>

3.  Create an Application class inside the src/main/java/io.github.bbop :
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-8.png" width="500" height="250" alt="">
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-9.png" width="225" height="75" alt="">
<br><br>

4. Replace the build.gradle file's contents with the below
<br><br>
    ```js
    buildscript {
        ext {
            springBootVersion = '2.0.0.RELEASE'
        }
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
        }
    }
    
    apply plugin: 'java'
    apply plugin: 'eclipse'
    apply plugin: 'org.springframework.boot'
    apply plugin: 'io.spring.dependency-management'
    
    group = 'io.github.bbop'
    version = '0.0.1-SNAPSHOT'
    sourceCompatibility = 1.8
    
    repositories {
        mavenCentral()
    }
    
    
    dependencies {
        compile('org.springframework.boot:spring-boot-starter-web')
        testCompile('org.springframework.boot:spring-boot-starter-test')
    }
    ```

5.  Add the below lines of code to Application.java
    
    ```js
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    @SpringBootApplication
    public class Application {
    
    	public static void main(String[] args) {
    		SpringApplication.run(Application.class, args);
    	}
    }
    ```

6.  Click on the _bootRun_ task from the _Gradle_ panel on the right hand side of Intellij.
This will start the spring-boot web app in the default port 8080.
<br><br>
<img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-10.png" width="300" height="250" alt="">
<br><br>


Now access localhost:8080 in any browser of your choice and you should see a page like below:
<br><br>
  <img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-11.png" width="500" height="200" alt="">
<br><br>

With this you have reached the first level of this exercise. Since you have copied the contents of build.gradle and
Application.java from the above blindly, let us try to understand what you did by copying these contents.

- build.gradle :
<br><br>
```js
    buildscript { // <-- This is for the build process itself, for the tasks made available by build.gradle
        ext {
            springBootVersion = '2.0.0.RELEASE'  // <-- what version of spring boot to use
        }
        repositories {
            mavenCentral()  // <-- From where to download the jars. Remember in the second para 
                            // of this question above - Is gradle/maven better than ant ? we read
                            // that one of the advantages of gradle is that we just specify the jar
                            // version and gradle can download it and add it to the build path.
                            // If you have any other location you need the jar from, you can specify
                            // it in the repositories. 
                            // Example (added inside repositories) :
                            //        maven {
                            //            url "https://plugins.gradle.org/m2/"
                            //       }
                            // See the below image for further clarity
        }
        dependencies {
            classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
            // <-- Jar that is needed in the classpath. Format - package:artifactId:versionName
            // For this excercise we need the above mentioned jar - 
        }
    
    // What are plugins for ?
    //  Plugins add new tasks (e.g. JavaCompile), domain objects (e.g. SourceSet), 
    //  conventions (e.g. Java source is located at src/main/java) 
    //  as well as extending core objects and objects from other plugins
     
    apply plugin: 'java' //This plugins add capability to compile java code
    
    apply plugin: 'org.springframework.boot'  // The Spring Boot Gradle Plugin provides Spring Boot support in Gradle, 
                                              // letting you package executable jar or war archives, run Spring Boot 
                                              // applications, and use the dependency management provided by spring-boot-dependencies
    
    apply plugin: 'io.spring.dependency-management' //A Gradle plugin that provides Maven-like dependency management and 
                                                    //exclusions.
    
    // Below information is what is used to build the fat jar of your app
    group = 'io.github.bbop'
    version = '0.0.1-SNAPSHOT'
    
    // Source language level
    sourceCompatibility = 1.8
    
    // This exactly like the comment above but this for that jars that the app depends.
    repositories {
        mavenCentral()
    }
    
    // What all jars are needed for compilation and running
    dependencies {
        compile('org.springframework.boot:spring-boot-starter-web')
        testCompile('org.springframework.boot:spring-boot-starter-test')
    }
```

Bonus : The global level dependencies and repositories sections list dependencies that required for building your source 
        and running your source etc.
        The buildscript is for the build.gradle file itself. So, this would contain dependencies for say creating RPMs,
        Dockerfile, and any other dependencies for running the tasks in all the dependent build.gradle.
        From [here](https://stackoverflow.com/questions/17773817/purpose-of-buildscript-block-in-gradle){:target="_blank"}
              
<br>
Dependency management in Gradle/Maven:
<br><br>
    <img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-12.png" width="400" height="300" alt="">
<br><br>
    
More detailed information on dependency management [here](https://docs.gradle.org/current/userguide/introduction_dependency_management.html){:target="_blank"}
