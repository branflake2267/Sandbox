#Maven GAE Plugin

##Google Project Page
The Team has managed to produce the next version of the maven-gae-plugin. 

<table>
  <thead>
    <tr><th>maven-gae-plugin</th><th>gae-runtime</th></tr>
  </thead>
  <tbody style="vertical-align:top">
    <tr style="vertical-align:top">
    <td>
    <ul>
       <li>Version 0.9.6</li>
       <li>Version 0.9.5</li>
       <li>Version 0.9.4<br/>
         Supports a way of adding arbitrary flags.</li>
       <li>Version 0.9.3<br/>
         Support for --application argument</li>
       <li>Version 0.9.2<br/>
         Code moved to github.</li>
       <li>Version 0.9.1<br/>
         Adds update-dos goal (issue 145).<br/>
         Fixes long standing cron goal issue (issue 117).</li>
       <li>Version 0.9.0<br/>
         Adds Backends Support (issue 135).</li>
       <li>Version 0.8.4<br/>
         Updates to some used maven plugins<br/>
         Fix to the way sourceEncoding is done (issue 120).</li>
       <li>Version 0.8.2<br/>
         Minor bug fixes.</li>
    </ul>
    ...
    </td>
    <td>
    <ul>
       <li>Version 1.7.5</li>
       <li>Version 1.7.4</li>
       <li>Version 1.7.0<br/>
         Targets Google App Engine 1.7.0<br/>
         Updates the datanucleus-appengine dependency to 2.0.1.1</li>
       <li>Version 1.6.4<br/>
         Targets Google App Engine 1.6.4</li>
       <li>Version 1.6.3<br/>
         Targets Google App Engine 1.6.3</li>
       <li>Version 1.6.2.1<br/>
         Targets Google App Engine 1.6.2.1</li>
       <li>Version 1.6.1.1<br/>
         Targets Google App Engine 1.6.1.1</li>
       <li>Version 1.6.1<br/>
         Targets Google App Engine 1.6.1</li>
       <li>Version 1.6.0<br/>
         Targets Google App Engine 1.6.0</li>
      </ul>
      </td>
    </tr>
  </tbody>
</table>


##Maven Generated site information
You can find a copy of the maven generated site information [here](http://www.kindleit.net/maven_gae_plugin/) and [here](http://maven-gae-plugin.github.com/maven-gae-plugin/).


##Issues
Issues are tracked in [github](https://github.com/maven-gae-plugin/maven-gae-plugin/issues).


##Boilerplate / Archetypes
[JAppStart](http://code.google.com/p/jappstart) is a very complete jump start for java GAE developers. [Spring Roo](http://www.springsource.org/roo) is also a great tool for setting up all the boilerplate code.

You can also find the following archetypes for your applications:
 * Plain JSP based example: 

        mvn archetype:generate -DarchetypeGroupId=net.kindleit -DarchetypeArtifactId=gae-archetype-jsp \
        -DarchetypeVersion=0.9.4 -DgroupId=com.myapp.test -DartifactId=testapp

 * Wicket based example

        mvn archetype:generate -DarchetypeGroupId=net.kindleit -DarchetypeArtifactId=gae-archetype-wicket \
        -DarchetypeVersion=0.9.4 -DgroupId=com.myapp.test -DartifactId=testapp

 * GWT based example

        mvn archetype:generate -DarchetypeGroupId=net.kindleit -DarchetypeArtifactId=gae-archetype-gwt \
        -DarchetypeVersion=0.9.4 -DgroupId=com.myapp.test -DartifactId=testapp


 * JSF based example

        mvn archetype:generate -DarchetypeGroupId=net.kindleit -DarchetypeArtifactId=gae-archetype-jsf \
        -DarchetypeVersion=0.9.4 -DgroupId=com.myapp.test -DartifactId=testapp


##Sample Maven Plugin Configuration

```xml
<properties>
     <gae.version>1.7.5</gae.version>
     <webappDirectory>${project.build.directory}/${project.build.finalName}</webappDirectory>
     <gae.home>
         ${settings.localRepository}/com/google/appengine/appengine-java-sdk/${gae.version}/appengine-java-sdk-${gae.version}
     </gae.home>
<propertiess>


<build>
    <plugin>
        <groupId>net.kindleit</groupId>
        <artifactId>maven-gae-plugin</artifactId>
        <version>0.9.5</version>
        <configuration>
            <sdkDir>${gae.home}</sdkDir>
            <!-- Add credentials to ~/.m2/settings.xml <id>appengine-credentials</id> -->
                <serverId>appengine-credentials</serverId>
                <splitJars>true</splitJars>
            </configuration>
            <executions>
                <execution>
                    <id>install-server-jar</id>
                    <phase>validate</phase>
                    <goals>
                        <goal>unpack</goal>
                    </goals>
                </execution>
                <execution>
                    <id>deploy</id>
                    <goals>
                        <goal>deploy</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

