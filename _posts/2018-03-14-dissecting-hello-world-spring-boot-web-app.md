---
layout: post
title:  "Dissecting Hello World Spring-boot Web App (to an extent ;)"
date:   2018-03-14
categories: technology java spring-boot
permalink: /:categories/:title
---

This post is to understand what it takes to build a simple hello world spring-boot web app and then dissect it to understand it.

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
    
    You should something like this in the console :

    ```
    7:14:50 PM: Executing task 'bootRun'...
    
    :compileJava
    :processResources UP-TO-DATE
    :classes
    :bootRun
    
      .   ____          _            __ _ _
     /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
    ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
     \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
      '  |____| .__|_| |_|_| |_\__, | / / / /
     =========|_|==============|___/=/_/_/_/
     :: Spring Boot ::        (v2.0.0.RELEASE)
    
    2018-03-21 19:15:07.138  INFO 96992 --- [           main] io.github.bbop.hwapp.Application         : Starting Application on Bishons-MacBook-Pro.local with PID 96992 (/Users/bishonbopanna/Downloads/hello-world-web-app/build/classes/java/main started by bishonbopanna in /Users/bishonbopanna/Downloads/hello-world-web-app)
    2018-03-21 19:15:07.141  INFO 96992 --- [           main] io.github.bbop.hwapp.Application         : No active profile set, falling back to default profiles: default
    2018-03-21 19:15:07.178  INFO 96992 --- [           main] ConfigServletWebServerApplicationContext : Refreshing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@c8e4bb0: startup date [Wed Mar 21 19:15:07 EDT 2018]; root of context hierarchy
    2018-03-21 19:15:07.933  INFO 96992 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
    2018-03-21 19:15:07.959  INFO 96992 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
    2018-03-21 19:15:07.959  INFO 96992 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/8.5.28
    2018-03-21 19:15:07.969  INFO 96992 --- [ost-startStop-1] o.a.catalina.core.AprLifecycleListener   : The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [/Users/bishonbopanna/Library/Java/Extensions:/Library/Java/Extensions:/Network/Library/Java/Extensions:/System/Library/Java/Extensions:/usr/lib/java:.]
    2018-03-21 19:15:08.050  INFO 96992 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
    2018-03-21 19:15:08.051  INFO 96992 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 875 ms
    2018-03-21 19:15:08.146  INFO 96992 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean  : Servlet dispatcherServlet mapped to [/]
    2018-03-21 19:15:08.155  INFO 96992 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'characterEncodingFilter' to: [/*]
    2018-03-21 19:15:08.155  INFO 96992 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
    2018-03-21 19:15:08.156  INFO 96992 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'httpPutFormContentFilter' to: [/*]
    2018-03-21 19:15:08.156  INFO 96992 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'requestContextFilter' to: [/*]
    2018-03-21 19:15:08.439  INFO 96992 --- [           main] s.w.s.m.m.a.RequestMappingHandlerAdapter : Looking for @ControllerAdvice: org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@c8e4bb0: startup date [Wed Mar 21 19:15:07 EDT 2018]; root of context hierarchy
    2018-03-21 19:15:08.500  INFO 96992 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error]}" onto public org.springframework.http.ResponseEntity<java.util.Map<java.lang.String, java.lang.Object>> org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.error(javax.servlet.http.HttpServletRequest)
    2018-03-21 19:15:08.501  INFO 96992 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error],produces=[text/html]}" onto public org.springframework.web.servlet.ModelAndView org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.errorHtml(javax.servlet.http.HttpServletRequest,javax.servlet.http.HttpServletResponse)
    2018-03-21 19:15:08.525  INFO 96992 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/webjars/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
    2018-03-21 19:15:08.525  INFO 96992 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
    2018-03-21 19:15:08.551  INFO 96992 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**/favicon.ico] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
    2018-03-21 19:15:08.651  INFO 96992 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
    2018-03-21 19:15:08.709  INFO 96992 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
    2018-03-21 19:15:08.712  INFO 96992 --- [           main] io.github.bbop.hwapp.Application         : Started Application in 16.846 seconds (JVM running for 17.19)
    ```

7.  Now access localhost:8080 in any browser of your choice and you should see a page like below. You are seeing this default message/page because
    we have still not added any service.
    <br><br>
      <img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-11.png" width="500" height="200" alt="">
    <br><br>

    #### With this you have reached the first level of this exercise. 

    Since you have copied the contents of build.gradle and Application.java from the above blindly, let us try to understand what you did by copying these contents.

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
        More detailed information on dependency management [here](https://docs.gradle.org/current/userguide/introduction_dependency_management.html){:target="_blank"}
        <br><br>
            <img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-12.png" width="400" height="300" alt="">
        <br><br>
            
     - Application.java :
         <br><br>
         ```js
         package io.github.bbop.hwapp;
         
         // Import statements for the APIs used in this class
         import org.springframework.boot.SpringApplication;
         import org.springframework.boot.autoconfigure.SpringBootApplication;
             
         @SpringBootApplication 
        // This is the most important part of this class that has to be understood since a lot of magic happens just
        // by this annotation. 
        // What is annotation in the first place ? Annotation is Metadata. Metadata is data about data. 
        // So Annotations are metadata for code.
        //
        // What does @SpringBootApplication do ? 
        // @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
        //
        // @Configuration : Spring Boot favors Java-based configuration. Although it is possible to call SpringApplication.run() 
        //                  with an XML source, it is generally recommend that your primary source is a @Configuration class.
        //                  
        //                  In simple terms -  This is to allow adding of bean defination in the main application class.
        //                  Annotating a class with the @Configuration indicates that the class can be used 
        //                  by the Spring IoC container as a source of bean definitions. That is by adding @Bean on a method and
        //                  you create/new a object and return it explicitly.
        //
        //                  @Configuration is not required, if you already pass the annotated class in the sources parameter when
        //                  calling the SpringApplication.run() method (below). It is required when you don't pass the annotated class explicitly, 
        //                  but it's in the package that's specified in the @ComponentScan annotation of your main configuration class.
        //                  For readability, classes that are even explicitly passed as sources may anyway be annotated with @Configuration 
        //                  - just to show the intentions more clearly. Do note that this class does not have any @Bean annotated methods.
        //
        // @EnableAutoConfiguration : Lot of springs opinionated approach is based on this annotation. What this does is that it tries 
        //                            to intelligently determine the default configurations for the beans that are in your class path and
        //                            applies the default configurations but if it finds that there is an explicit configuration in any of 
        //                            the properties file it will use it.  Auto-configuration is always applied after user-defined beans 
        //                            have been registered. Read its Java docs, very explainatory.
        //
        // @ComponentScan : This configuration is to tell spring to look for packages to scan for components. Any class which is annotated
        //                  with @Component will be scanned and registered by spring. Classes annotated with @Configuration are also candidates 
        //                  for component scanning as @Configuration annotation is meta-annotated with @Component. You can include or exclude
        //                  package from being looked into by spring using excludeFilters or includeFilters for @ComponentScan 
         
         public class Application {
             
            public static void main(String[] args) { // main method, this the first point of execution of the app
                SpringApplication.run(Application.class, args);
            }
         }
         ```
       
    <br><br>  
    #### Now that we understand the above let us move to the second stage of this exercise :

8.  Add a "controllers" package under "io.github.bbop" and create HWAppController.java and add the below code to it. 
    Stop + Clean + Start (bootRun) your App.
    
    ```js
    package io.github.bbop.controllers;
        
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    
    /**
     * @author bishonbopanna
     */
    @RestController // This a convenience annotation that does nothing more than adding the @Controller
                    // and @ResponseBody annotations.
                    // In simple terms - this annotation takes the return value and add it to the http response object directly.
    public class HWAppController
    {
        @RequestMapping("/dissect-hello-world") // This annotation it to configure your service path/URI
        public String someMethod() {
            return "You have now dissected Hello World spring-boot web app (to an extent ;))";
        }
    }
    ```

8.  Access localhost:8080/dissect-hello-world in your browser. Do you get the return string from the above service ?

    Nope. You will still see the same Whitelable Error Page. What are we missing ?
       
       In the above step we created a package - "controllers" and added the HWAppController to this package. 
       Now with this spring-boot does not know that it has to associate the HWAppController to a dispatcher servlet that dispatches the service
       to your method.
       
    Two options to fix this :
    
    a.  In the Application.java which is the  class containing the main method, add @ComponentScan(basePackages = "io.github.bbop") right after
                @SpringBootApplication annotation. This @ComponentScan with basePackages tells spring to scan all packages under io.github.bbop and associate
                it to the servlet dispatcher. 
                Servlet Dispatcher - is a listener that takes the incoming request and delegates it to the right method, in the right controller, using 
                the path in the URI
                
    Application.java:
    
    ```js
    package io.github.bbop.hwapp;
            
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.context.annotation.ComponentScan;
    
    @SpringBootApplication
    @ComponentScan(basePackages = "io.github.bbop") // ADD THIS LINE
    public class Application {
    
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    }
    ```
    
    b.  Move the HWAppController into "io.github.bbop.hwapp" package and since the Application.java resides in the same package and since it has
        @SpringBootApplication annotation which internally has @ComponentScan, the association to dispatcher servlet happens automatically
        
        
        
9.  Stop + Clean + Start (bootRun) your App. Access localhost:8080/dissect-hello-world in your browser. You should see the below:
<br><br>
  <img src="./../../../resources/images/technology/java/hello-world-web-app/hwwa-13.png" width="450" height="100" alt="">
<br><br>
   
#### With this you have reached the second and last level of this exercise. Congratulations! Hope this was useful!!!
 