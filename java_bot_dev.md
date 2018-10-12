# Java Bot Primer

This is intended for  developers venturing into Java Bot [source code]( https://github.com/Microsoft/botbuilder-java).

## Dependencies
**Java**

​   *Bot SDK V1.8 [JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

​   *Autorest for Java V1.7 

​   *(Note: Most all Azure client libraries are using version 7)

**Build**

​   *Build: [Maven](https://maven.apache.org/what-is-maven.html)

​   *Public Repository: [Maven Central](https://search.maven.org/)

​       (Publish is manual)

​     *CICD: [Travis](https://travis-ci.org/Microsoft/botbuilder-java)

​       *Triggers on each commit on all branches.

​       *Does not publish to Maven Central.

​       *No code coverage stats

**Web Framework**

​      *Current proposal :  [Spring Boot](http://spring.io/projects/spring-boot) (Works with Tomcat. Jetty or Undertow)

**Test**

​   *[JUnit](https://junit.org/junit5/)

**Logging**

​   *[Log4J2](https://logging.apache.org/log4j/2.x/)

**Json Serialization**

​   *[Jackson](https://github.com/FasterXML/jackson)

**Http Client**

​   *[OkHttp](http://square.github.io/okhttp/)

​   *[Retrofit](https://square.github.io/retrofit/)

**Autorest**

​   *[Autorest](https://github.com/Azure/autorest-clientruntime-for-java) Java flavored.

**Samples/Template Generation**

​   *[Maven Archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html)

​   *Mark Barbera built a archetype using the existing Echobot as the template!.

​   *Spring-boot has their own  archetype/template system.  They've granted all of Microsoft Azure two slots for templates.  If we want a great deployment experience  with Spring-Boot we'll need to  work with the Azure team or work with Spring to get more slots.

​   *See Ruth for more details
   

## Random Notes
   **Editor/IDE:** You can use IntelliJ/Eclipse as your editor.  One thing to consider, the Azure integration appears to work better with Intellij.

   **Azure Integration:** With [Azure Intellij integration](https://plugins.jetbrains.com/plugin/8053-azure-toolkit-for-intellij), you can publish bots from the IDE as Web APP/Docker Container.  [Eclipse Azure integration](https://docs.microsoft.com/en-us/java/azure/eclipse/azure-toolkit-for-eclipse?view=azure-java-stable) appears to have some issues at the moment.

   **Azure Integration:** The Azure Web App appears to be using Tomcat as the default server inside a container.

   **Azure/Spring-boot:** Non-polished sample can be had  [here](https://github.com/daveta/java_spring_bot).  Implements echobot in Spring-Boot and deploys to Azure using Web App.

   **Autorest:** In practice, people add properties to Activity are outside the definition of our  [wire format](https://github.com/Microsoft/BotBuilder/blob/master/specs/botframework-activity/botframework-activity.md).  This enables flexibility, but introduces a challenge for our serialization.  Autorest for C# generates a separate dictionary that collects these  properties.  There is a request for Autorest for Java to add an equivalent feature, but it has not been added.  To that end, we hand modify the generated code.
As a result, turning crank on Autorest requires hand edits.  I believe there's another case that required hand edits which i'll document when I review.

   **async:** No formal support for async/await in Java8.

   **async:** The company EA has [built an attempt](https://github.com/electronicarts/ea-async) on top of [CompleteableFuture](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html).

   **async:** After failed attempts, current approach is convert code as  synchronous and convert to CompletableFuture.

   **async:** Trivia: When toying with CompletableFutures, it uses underlying thread pool.  The pool defaults to *1* thread.  Just something to keep in mind. Also need to understand entire underlying stack we adopt and if that impacts our decision on thread pools.

   **async:** Autorest [has adopted the react framework](https://github.com/ReactiveX/RxJava) for it's model.

   **async:** Autorest not moving to Java8 in near future, blocking any CompletableFuture adoption.

   **conversion:** There is code in botbuilder-java branch "v4.1".  I used a tool to convert the entire BotBuilder project from C# to Java on10/9/2018.  This is best starting point as comments and formating carried over.

   **conversion:** Common cases: string.IsNullOrEmpty => StringUtils.isBlank :)

   **Feature creep?** We could create an equivalent of the asp.net core/webapi integration layer to smooth rough edges on Springboot

   **Storage:** Jdbc appears to be a popular interface for databases, but [Microsoft not supporting](https://www.oracle.com/technetwork/java/index-136695.html), including [latest Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-sdk-java).
