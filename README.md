# tcguru

## About This Course

Welcome to this course, about **Tomcat 9 (TC9)** on **Red Hat Enterprise Linux 8 (RHEL8)**.

# What Is Tomcat

Tomcat is a pure Java HTTP web server environment in which Java code can run. It is open source and available to run on many different platforms, as long as they support Java.

The **Apache** Tomcat software is an implementation of **Java Servlet**, **JavaServer Pages**, **Java Expression Language**, and **Java WebSocket** technologies.

<details>
  <summary>Click here to view the different technologies.</summary><br>

**Java Servlet**

It is a software component of Java that extends the capabilities of a server.

* The most common use is implementing applications hosted on web servers.

* A **servlet** can add dynamic content to a web server using the Java platform.

* Content is normally HTML, but could be something else such as XML.

* Requires a _web container_ (servlet container) to run.

**JavaServer Page (JSP)**

It is a group of technologies that helps a developer create dynamically generated web pages.

* It is a high-level abstraction of Java servlets.

* JSPs are translated into servlets at runtime.

* They are cached and reused at run time.

* The web pages are based on HTML, XML or other types.

* To deploy and run JSPs, you need to use something compatible (a servlet container) such as Tomcat.

* They must be executed within a Java virtual machine (JVM).

**Java Expression Language**

The Java Expression Lnaguage (JEL) is a programming language mostly used in Java web applications for embedding expressions into web pages.

An expression language is designed to make it easy to access application data stored in **JavaBeans** components. It was originally called **SPEL (Simplest Possible Expression Language)**.

**Java Websocket**

A _websocket_ is a communications protocol which provides full-duplex communication over a single TCP connection.

* It can send content to the client without first getting a request from the client.

* It is not the same as HTTP, though it is designed to work over HTTP ports 80 and 443.

* A websocket enables interactions between a web browser and a web server. In this case with Tomcat.

* It is good for low-latency applications.

**Open Source**

Tomcat is licensed under the Apache License. More information about the license can be found at https://www.apache.org/licenses/.

The Apache License allows users to use the software for any purpose, to distribute it, to modify it, and to distribute modified versions of the software under the terms of the license without concern for royalties.

</details>

# The Services Tomcat Provides

So what can Tomcat do? Tomcat is an open source _web application server_ licensed under the Apache License.

* It is called a _web application server_, not an _application server_, due to only being able to work with `.war` files. One of the things it does is to execute servlets and render up webpages.

* Some people will say it's not an application server, since it won't run `.ear` files, but some say it can run `.ear` files with additional software.

* It is not **Java EE** certified. Smaller applications used with Tomcat will work well, while others require the full use of a **Java Platform Enterprise Edition** application server.

<details>
  <summary>Click here to view WAR files.</summary><br>

**WAR Files Only, Please**

For Tomcat, we use **WAR** files (**Web Application Resource**), not **EAR** files (**Enterprise Application aRchive**).

* Tomcat is a servlet container so is a "pure Java" web server environment. It's an environment that responds to HTTP requests, it is designed for WAR files, not for Java applications.

* If you need Java applications, then **JBoss** may be a better option for you. It also has a servlet container.

A WAR file is a package that contains the following:

* JAR-files
* Java servlets
* Java classes
* XML files
* JavaServer pages
* Libraries
* Static web pages
* Other resources

Note that a WAR file can be digitally signed. This is so people can determine where the source code has come from.

**WAR File Contents**

A WAR file has some special files and folders inside of it.

* The `/WEB_INF` directory contains a file called `web.xml`. This file defines the web application's structure.

* The `web.xml` file is not strictly necessary if the application is only serving JSP files.

* If the web application uses servlets, then the `web.xml` tells the servlet container which servlet should get the request.

* The `web.xml` is also used to define certain variables for reference inside the servlets, and it defines environment dependencies, e.g a mail session to send email.

Let's have a look at a portion of a `web.xml` file and see what it contains. The `servlet-mapping` tag associates a URL endpoint with a Java servlet.

```xml
<web-app>
  <servlet>
    <servlet-name>HelloServlet</servlet-name>
    <servlet-class>mypackage.HelloServlet</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>HelloServlet</servlet-name>
    <url-pattern>/HelloServlet</url-pattern>
  </servlet-mapping>
```

**WAR File Pros and Cons**

There are some advantages for using WAR files.

* It promotes easy testing and deployment.

* All Java EE containers support WAR files.

* You can set environment specific variables with external properties files. For a development environment you might point to a dev target, and for a production environment you would point to a prod target. This helps you verify that code is tested and working.

There are some disadvantages however.

* Minor changes must be repackaged and redeployed.

* It can be inconvenient to stop and restart the web server.

</details>

<details>
  <summary>Click here to view Tomcat uses.</summary><br>

**Tomcat and Its Uses**

Tomcat is easy to install. It is often used with _load balancers_ as the front end.

* You can use Apache web server with `mod_proxy` or Varnish, to forward traffic to port `8080`.

* By default it uses port `8080`, but the port can be changed in configuration files.

* You can configure **SSL/TLS** with Tomcat, most installations that require SSL/TLS will use a separate front end and direct traffic as required.

* It can be set to start and stop as a service, and it requires Java.

* Tomcat has a web-based administration console: `http://localhost:8080/manager`.

* You need to add users before they can access the administrative features.

* Tomcat deployment is easy. Place the `.war` files into the `/webapps` folder.

</details>

# Tomcat Administrator

The Tomcat Administrator is normally also the server administrator, though the tasks may be separated.

The administrator will get the application from the developer.

* If there are problems with the application, the developer would be engaged to fix any issues.

* In an ideal world, only well-tested and documented applications would be moved into production.

<details>
  <summary>Click here to view Tomcat day-to-day.</summary><br>

**Tomcat Day-to-Day**

The tasks you may be expected to perform as a Tomcat Administrator might be some or all of the following:

* Monitor the existing Tomcat servers:
  * Memory usage
  * Java resource usage
  * Disk space
  * Logs for errors
* Day to day managing of the applications:
  * Adding new `.war` files
  * Changing or removing `.war` files
  * Updating information for databases or shared resources
  * Updating the **JDBC (Java Database Connectivity)** framework
* User and role management:
  * Locally via configuration files
  * Via a realm (database of usernames, passwords)
  * Other (via plugins or code changes)
* Automating tasks:
  * Scripting or coding for repetitive tasks
  * Continuous integration, e.g via Jenkins or another method
* Optimizing environment:
  * Adjusting parameters for open files
  * Garbage collection
  * Management of memory

</details>

# Comparisons Between Java Application Servers

There are many solutions available if you want to use Java web applications or Java servlets.

* Tomcat
* JBoss EAP
* WebLogic

This repo itself is about Tomcat but in this section we discuss two of the others, and give some more information about those solutions.

<details>
  <summary>Click here to view the other solutions.</summary>

## JBoss EAP

**JBoss EAP** is a subscription based, open source Java EE based application server runtime.

* It is free for use in a development environment.

* Unlike Tomcat, there is a cost for use in a production environment.

* There is a free community edition called **WildFly**.

* It is a certified Java Enterprise Edition application server, so it has all the classes and dependencies than an EE application needs in order to run.

## WebLogic

**WebLogic** was developed and is licensed by **Oracle**.

* Closed source

* Can be expensive

* Typically used in large enterprise environments

* Integrates well with other Oracle products

* Can be difficult to setup and maintain

</details>

# Installing on Linux

In this section we will install Tomcat 9 onto Red Hat Enterprise Linux 8. First we become the root user and check and install updates:

<details>
  <summary>Click here to install Tomcat 9 on RHEL8.</summary><br>

```sh
sudo su -
yum update
yum-config-manager --enable rhel-7-server-optional-rpms
```

Next we install java-11-openjdk-devel package:

```sh
yum install java-11-openjdk-devel
```

We check the version of Java:

```sh
java --version
```

Then we go to a [webpage](https://tomcat.apache.org/download-90.cgi) to get the latest version of Tomcat 9. We copy the link for `tar.gz` file to the clipboard. 

Before we can get them, we need to ensure we have wget installed. We might as well also install some other software that will get used later. (Note: we use yum install here but could also use dnf install):

```sh
yum install wget tree vim 
wget <tomcat-tar-gz-file>
``` 

Note: Below is a link to a mirror that should be ok. It is preferable to use the link copied to the clipboard earlier:

```sh
wget http://mirror.cogentco.com/pub/apache/tomcat/tomcat-9/v9.0.31/bin/apache-tomcat-9.0.31.tar.gz
```

Now we go to the folder we want to put Tomcat into, and extract the downloaded file to the current location. Note: Your filename may be slightly different than what I have here.

```sh
cd /usr/local
tar -xvf /root/apache-tomcat-9.0.31.tar.gz
```

Now we use the mv command to change the folder name.

```sh
mv apache-tomcat-9.0.31 tomcat9
```

Now we add the tomcat user as a system account. This means we don't need to do anything special for SELinux, as the system account will allow things to just work as we require. If you don't use a system account, you may need to manually fix things up for use with SELinux:

```sh
useradd -r tomcat
```

Now we need to change the permissions of the tomcat folder so the tomcat user can use it:

```sh
chown -R tomcat:tomcat /usr/local/tomcat9
```

Now we need to create the tomcat service. We use Vim to edit the file, but feel free to use the editor of your own choice:

```sh
vim /etc/systemd/system/tomcat.service
````

Add these contents to the file:

```
[Unit]
Description=Apache Tomcat
After=syslog.target network.target

[Service]
Type=forking
User=tomcat
Group=tomcat

Environment=CATALINA_PID=/usr/local/tomcat9/temp/tomcat.pid
Environment=CATALINA_HOME=/usr/local/tomcat9
Environment=CATALINA_BASE=/usr/local/tomcat9

ExecStart=/usr/local/tomcat9/bin/catalina.sh start
ExecStop=/usr/local/tomcat9/bin/catalina.sh stop

RestartSec=12
Restart=always
[Install]
WantedBy=multi-user.target
```

Now we get the system to recognize a new service is available, start and enable the service, then check its status:

```sh
systemctl daemon-reload
systemctl start tomcat
systemctl enable tomcat
systemctl status tomcat
```

Check that Tomcat works by going to your server's web page on the port `8080`:

```
http://<YOURSERVERIP>:8080
```

Let's add a user for the web console:

```sh
cd /usr/local/tomcat9/
vim conf/tomcat-users.xml
```

Go to the bottom of the file, and put the following just before the `<\/tomcat-users>` end block. Don't forget to change the `YOURPASSWORDHERE` to be your own password:

```xml
<role rolename="admin-gui,manager-gui"/> 
<user username="admin" password="YOURPASSWORDHERE" roles="admin-gui,manager-gui"/>
```

Now you need to allow access to the management web pages from the internet. If you know what you're doing, you could just allow access from your own IP address, but that is not covered in these written instructions:

```sh
vim webapps/manager/META-INF/context.xml
```

Change the following line:

```xml
allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
```

It should read:

```xml
allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1 |.*" />
```

Now restart Tomcat:

```sh
systemctl restart tomcat
```

Now go to your Tomcat web console and use the user you created to log in.

You now have a working Tomcat installation.

Thank you.

</details>

# Installing on Windows 2019 Server

In this section we will discuss and show how to install Tomcat 9 onto Windows 2019 Server. These links may be of use:

* [Apache Tomcat install notes](https://tomcat.apache.org/tomcat-9.0-doc/setup.html#Windows)

* [Apache Tomcat download page](https://tomcat.apache.org/download-90.cgi)

* If you need to download Java, then once you have registered with Oracle you can [download the software for Windows](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)

# The Configuration Files

In this lesson we will discuss these files located in the `./conf` folder:

* `catalina.policy` - security policy for the Catalina Java class
* `catalina.properties` - Java properties for the Catalina class
* `context.xml` - context information for every web application running
* `jaspic-providers.xml` - For using **JASPIC** with a web application
* `logging-properties` - logging configuration

There are many references to **Catalina** in Tomcat.

* Tomcat's core component is Catalina.
* Tomcat servlet specification comes from Catalina.
* When you start Tomcat, you actually start Catalina.

The main files `server.xml`, `web.xml` and `tomcat-users.xml` have sections specific to them.

<details>
  <summary>Click here to view the configuration files.</summary><br>

**File catalina.policy**

The file `catalina.policy` is a default security policy for Tomcat, and it uses syntax defined in JEE specifications.

**File catanlina.properties**

The file `catalina.properties` is a Java properties file for the Catalina class and it contains security related information. It also contains some cache settings, and you may edit some settings to tune performance.

**File context.xml**

The file `context.xml` is used to configure Tomcat context information, which is loaded for every web application running. Some settings, like persistence, may be changed if needed.

**File jaspic-providers.xml**

The file `jaspic-providers.xml` is a **Java Authentication Service Provider Interface for Containers**. It can be used for **Oauth**, **OpenID**, or other mechanisms.

It is used for external authentication, outside of Tomcat, and credentials are managed elsewhere.

**File logging-properties**

The file `logging-properties` configures logs for Tomcat. It uses **JULI**, a packaged renamed fork of **Apache Commons Logging**, instead of JDK's logging implementation.

Note that logs are located under `./logs` and don't auto rotate. You should set up `logrotate` or some other method to clean them out.

</details>


# Adding Users to Tomcat

The `tomcat-users.xml` is used to define the default parameters for the users on the Tomcat. It contains a list of user names, roles and passwords.

<details>
  <summary>Click here to view the roles and commands.</summary>

## Roles

There are several roles that can be added in the `tomcat-users.xml` file. 

These are the roles for the Tomcat Manager application:

* **manager-gui** - The HTML interface
* **manager-status** - The Server Status page only
* **manager-script** - For use with a tools-friendly plain text interface, and Server Status page.
* **manager-jmx** - The **JMX (Java Management eXtensions)** and also the Server Status page

These are the roles for the Host Manager application. With the Host Manager you can use scripted commands.

* **admin-gui** - Access to the HTML GUI and the status pages
* **admin-script** - Allows access to the text interface and the status pages

Note that from Tomcat 7+, the roles required to use the Host Manager application were changed from the single admin role to both the roles.

## Scripted Commands

You can script commands to the Tomcat interface:

```sh
curl -u <user>:<pass> http://localhost:8080/host-manager/text/list
```

The supported commands:
* list
* add
* remove
* start
* stop
* persist

A good resource can be found on the Tomcat Documentation page. This URL discusses [the Host Manager and how to use it](https://tomcat.apache.org/tomcat-9.0-doc/host-manager-howto.html).

</details>

<details>
  <summary>Click here to view digest and other authentications.</summary>

## Digest Authentication

You can put a password hash, rather than plain text passwords, into the configuration file. Changes need to be made to the `./conf/server.xml`.

You create a digest password using `./bin/digest.sh`, copy the digested password to the `./conf/tomcat-users.xml` file, and restart Tomcat.

Change the `./conf/server.xml` from this:

```xml
<Realm className="org.apache.catalina.realm.LockOutRealm">
  <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
    resourceName="UserDatabase" />
</Realm>
```

To this:

```xml
<Realm className="org.apache.catalina.realm.LockOutRealm">
  <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
    resourceName="UserDatabase">
    <CredentialHandler className="org.apache.catalina.realm.MessageDigestCredentialHandler" 
      algorithm="sha-512" />
  </Realm>
</Realm>
```

To create the `sha-512` key for a password of `password1` (from the `tomcat` folder):

```sh
./bin/digest.sh -a sha-512 -h org.apache.catalina.realm.MessageDigestCredentialHandler password1
````

This returns a string response `password1:<hash>`. Then edit the `./conf/tomcat-users.xml` and replace this line:

```xml
<user username="admin" password="password1" roles="admin-gui,admin-script,manager-gui"/>
```

With the following (note the `<hash>` key copied from the previous step):

```xml
<user username="admin" password="<hash>" roles="admin-gui,admin-script,manager-gui"/>
```

Restart Tomcat and use curl to test:

```sh
curl -u admin:password1 http://localhost:8080/host-manager/text/list
```

## Other Authentication

You can use other external methods to allow user access. Some Tomcat installations use databases for storing user data.

You can also use **LDAP** or **Windows Active Directory** for user management. This URL has more information about [realms and using tools such as LDAP](https://tomcat.apache.org/tomcat-9.0-doc/realm-howto.html)

</details>

# The server.xml file

The `server.xml` is Tomcat's main configuration file. It is installed as part of the installation process.

It comes with defaults already set. Using the defaults, Tomcat should run with minimal configuration.

The `server.xml` is used to configure the structure of the Tomcat server. There are several categories inside this configuration file we need to be aware of:

* Top-Level Elements
* Connectors
* Containers
* Nested Components
* Cluster Elements

These categories and their attributes fine tune functionalities.

<details>
  <summary>Click here to view the server.xml categories and their attributes.</summary>

## Top-Level Elements

The main configuration file has the following top-level elements:

* `<Server>` is the root element of the entire configuration file
* `<Service>` represents a group of Connectors that is associated with an Engine.

## Connectors

Connectors are the interface between external clients sending requests and the response back from a particular service:

* **HTTP/1.1** Connector - Represents an HTTP/1.1 Connector, and provides stand-alone web server functionality.

* **HTTP/2** Connector - Represents an Upgrade Protocol component that supports the HTTP/2 protocol.

* **AJP** Connector - Communicates with the AJP Protocol and allows you to integrate with an installation of Apache.

## Containers

Containers are components that process incoming requests. They direct requests to the correct processing mechanism.

Components are:

* `<Engine>` - Requests for a service from Catalina
* `<Host>` - Requests for a particular virtual host
* `<Context>` - Requests for a specific web application

It's not recommended to use `<Context>` elements in `server.xml` since they are only reloaded on restart.

## Nested Components

These components can be nested inside the element for a container. See Nested Components in the documentation for details.

An important point to highlight that's not mentioned in the documentation is the **Executor**, a pool of shared threads between components. It is a nested element to the `<Service>` element.

## Cluster Elements

Tomcat has the ability to use clustering. This can provide:

* Session replication
* Context attribute replication
* Cluster wide **WAR** file deployment

It is extensible and has many options which gives a lot of control over clustering. The `<Cluster>` element can be inside the `<Engine>` or `<Host>` container.

</details>

# The web.xml file

In this lesson we discuss the ./conf/web.xml file. We briefly touch on the application's web.xml also and discuss when to use one or the other.

We show examples of the files and some of the default entries in them.





Remote Access to the Tomcat Manager GUI

In this lesson we discuss remote access to your Tomcat server.

We show which configuration file to edit and where to make your changes. We also see the different Valve configurations that can be used to control access to Tomcat.





Changing the Port for Tomcat

There are many situations when you can't use the default port of 8080 for Tomcat. In this lesson, we look at how we can change which port Tomcat uses.

We also see what happens when you use a port that is already in use.





Apache as a Proxy to Tomcat

In this lesson we discuss using a proxy as a front end to Tomcat. We talk about several options available and why you might use them.

We discuss how to set up and use Apache web server as a proxy or front end to Tomcat.

To set up Apache as a proxy, we edit the following file:

/etc/httpd/conf.d/tomcat_manager.conf
And we place this inside it:

<VirtualHost *:80>
    ServerAdmin root@localhost
    ServerName kevinpjames5c.mylabserver.com
    DefaultType text/html
    ProxyRequests off
    ProxyPreserveHost On
    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/
</VirtualHost>
We also modify the following file:

/usr/local/tomcat9/conf/server.xml 
This text will be changed:

 <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
It looks like the following when we're done:

 <Connector port="8080" proxyName="myserver.mycompany.com" proxyPort="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
If you have SELinux running on the server, it needs to be set to allow this proxy to take place. We make the following changes to allow this:

setsebool -P httpd_can_network_connect 1
setsebool -P httpd_can_network_relay 1
setsebool -P httpd_graceful_shutdown 1
setsebool -P nis_enabled 1 
Then we restart the Apache web server and test to see if it works by going to our server on port 80.





Load Balancing


In this lesson we discuss load balancing, and why you might need it. We'll look at using the Apache web server as a load balancer front end to two Tomcat instances.

For those who wish to follow along, this lesson involves three servers in the Cloud Playground, one running the Apache web server, and two running Tomcat. The latter two have been configured according to how the lessons on setting up Tomcat specified.

Note that all of the following tasks are performed as the root user.

Install Apache
On what will be the load balancer, we need to install the Apache web server.

[root@apache-server ]# dnf -y install httpd vim

[root@apache-server ]# systemctl enable httpd
[root@apache-server ]# systemctl start httpd
[root@apache-server ]# systemctl status httpd
You should then test to ensure you can see the default Apache web page on that server.

Then we need to configure the Apache web server as a load balancer, so we have to add some modules and set up the balancer.

Edit the /etc/httpd/conf/httpd.conf file, then go to the bottom of it and add the following before the line that says IncludeOptional conf.d/*.conf

LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
LoadModule proxy_http_module modules/mod_proxy_http.so

<IfModule proxy_module>
ProxyRequests on
ProxyPass /examples balancer://mycluster stickysession=JSESSIONID
ProxyPassReverse /examples balancer://mycluster stickysession=JSESSIONID

<Proxy balancer://mycluster>
BalancerMember http://YOUR_OWN_IP_1:8080/examples route=tomcat1
BalancerMember http://YOUR_OWN_IP_2:8080/examples route=tomcat2
</Proxy>

</IfModule>
Don't forget to set the IP address to your own server's internal IP address.

Configuring the Tomcat Servers
Go to your first Tomcat server and either perform the tasks as the root user, or preface them with the sudo command:

[root@tomcat1 ]# cd /usr/local/tomcat6
Edit conf/server.xml.

Change this line of text:

<Engine name="Catalina" defaultHost="localhost" >
It should read:

<Engine name="Catalina" defaultHost="localhost" jvmRoute="tomcat1">
Save the file, and restart the Tomcat server:

[root@tomcat1 ]# systemctl restart tomcat
Now go to your second Tomcat server and either perform the tasks as the root user, or preface them with the sudo command:

[root@tomcat2 ]# cd /usr/local/tomcat6

Edit conf/server.xml.

Change this line of text:

<Engine name="Catalina" defaultHost="localhost" >
It should read:

<Engine name="Catalina" defaultHost="localhost" jvmRoute="tomcat2">
Save the file and restart Tomcat:

[root@tomcat1 ]# systemctl restart tomcat
Go back to the Apache web server.

If you have SELinux running on the server, it needs to be set to allow this proxy to take place. We make the following changes to allow this, or disable SELinux:

[root@apache-server ]# setsebool -P httpd_can_network_connect 1
[root@apache-server ]# setsebool -P httpd_can_network_relay 1
[root@apache-server ]# setsebool -P httpd_graceful_shutdown 1
[root@apache-server ]# setsebool -P nis_enabled 1
Then we restart the Apache web server again.

Go to the web page for this server, and paste in the following URL. Note that you will need to put your own IP address where it says YOUR_OWN_IP.

http://YOUR_OWN_IP/examples/servlets/servlet/SessionExample

You should be able to see the sample application (provided the example applications have been installed with the default installation).





Server Status


In this lesson we discuss the Tomcat Management GUI, and in particular the Server Status application.

This is a default application that comes with Tomcat, and is used to help you manage your Tomcat server and applications.





Manager App


In this lesson we discuss the Manager App from the Tomcat Management GUI.

This is a default application that comes with Tomcat and is used to help you manage your Tomcat server and applications.

You can use this to start, stop, undeploy, or deploy war files to your Tomcat server.

You can also perform some diagnostics, and check for leaks.




Host Manager

In this lesson we discuss the Host Manager App in the Tomcat Management GUI.

This is a default application that comes with Tomcat and is used to help you manage your Tomcat server and applications.

You can use this to map a virtual host name to your Tomcat applications, which allows you to connect to them as a server or hostname, instead of via the Tomcat hostname.

To make use of persistence (being able to save additions you make via the GUI) you need to add some code to your server.xml file.

Go to your server and edit the server.xml file (it is inside the ./conf folder).

Find the section of the file that has the Listener classes.

Add the following change after the other Listeners:

 <!-- Enable Persistence -->
   <Listener className="org.apache.catalina.storeconfig.StoreConfigLifecycleListener"/>

Save the file and restart Tomcat.





Virtual Host Management Non GUI

In this lesson we discuss adding a virtual host without using the Tomcat Management GUI.

You can use virtual host's to map a host name to your Tomcat Applications. This allows you to connect to them as a server or hostname, instead of via the Tomcat hostname.

This is the code that is used in this lesson:

     <Host name="test.acloud.guru"  appBase="test"
            unpackWARs="true" autoDeploy="true">

        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="test_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

      </Host>

To understand how to use this code, please follow along in the lesson.





WAR Files

In this lesson we discuss WAR files, which are web application resource files. There are other names they are known by, such as web application archives.

We discuss their uses and contents, and that they are compressed. We also discuss what some of the files are called, what they are used for, and whether some of them are needed.

We show you can uncompress them so changes can be made, then how to recompress them and make them ready for use on your Tomcat server.




Deploy via the Web GUI

In this lesson we discuss using the Tomcat Management GUI to upload applications.

There are several methods for getting an application deployed using the GUI.

In this lesson we show how to deploy an application uploaded via the browser. We also show how to deploy an application that's located on the Tomcat server.

In this lesson we show you how to use parallel deployment via versioning your Tomcat application. We show how this is stored on the Tomcat server.



Deploy via the CLI

In this lesson we cover deploying your application from the Command Line Interface (CLI). Using standard Linux commands, you can deploy or undeploy your applications quickly and easily.

In the lesson we show that an application that has been deployed can be easily replaced by a newer application, and the new application will automatically be deployed.



Static vs Dynamic Deployment

In this lesson we cover what static versus dynamic deployment means, and how you perform both types.

One of the items we discuss is the sequence of application deployment when you start your Tomcat server.

We show you how to deploy an application that has been exploded, and what happens when you add or remove your application and start Tomcat.

We also discuss other methods to deploy your applications on Tomcat.




Backups

In this lesson we cover what sorts of things you need to back up on your Tomcat server.

We discuss my you might not need to make backups.

We show how easy it is to copy back an application that has been undeployed when your code is in source control.

In this lesson we also do something to break the Tomcat manager, and then restore from a backup.




Diagnostics

In this lesson we will look at diagnostics and troubleshooting processes for your Tomcat installation. We will discuss methods to focus on which will help determine what your problem might be.

We also discuss logs as they apply to troubleshooting, and mention some other lessons in the section of the course that can help you in your efforts to resolve issues.





Logging

In this lesson we discuss Logging in Tomcat and JULI. We talk about the default log files for Tomcat, where they are, and what they show.

We will look at how to add a log for a virtual application, and what the options are. We'll examine the patterns used for this log, then we'll connect to a server and show examples.

Information about the patterns you can use for logs in Tomcat can be found here:

https://tomcat.apache.org/tomcat-9.0-doc/api/index.html

Search for AccessLogValve.




Garbage Collection

In this lesson we discuss what garbage collection is and how it's needed by Java. We will look at how to enable verbose logging, and how to enable parallel garbage collection.

We will look at the entries required in the bin/setenv.sh file.

We also show it in action by enabling verbose logging, and then starting some applications concurrently that use resources and force the garbage collection to occur. We'll watch this happen in our log.




JVM Tuning

In this lesson we discuss adjusting the heap size to increase performance.

We will look at heap sizing, and then PermGen space (what it is and how you set it).

In this lesson we also show examples of making changes to your server, and how you can recognize the changes have taken place.





ULimits and Fixed Heap Size

In this lesson we discuss setting ulimits for your users, and also what the fixed heap size is. We discuss why you would want to use a fixed heap size for your production Tomcat environments.

In the server portion of this lesson we show you how to set ulimits for your Tomcat user, and we show you how to set a fixed heap size of 2gb for the Tomcat server. We also show the changes to memory in the Tomcat Manager GUI.






Using JConsole

In this lesson we discuss using a tool called JConsole to examine what is happening with our JVM and its resources.

JConsole is free with the Java JDK, and it requires a graphical interface to be used. It allows you to monitor the resource usage for all your Java applications, including Tomcat and your web applications.

We'll look at this tool, and see an example of it being used on a Tomcat server.





Create and Analyze Java Heap Dumps

In this lesson we discuss using a tool called jmap to create a heap dump on our Tomcat Server.

It is free with the Java JDK, and doesn't require a graphical interface to use. It only requires the Java JDK to be installed.

Once we have our heap dump, we'll transfer it to a local computer.

Eclipse has a memory analyzer tool that you can download. It reads your dumped file and helps you analyze it.

You can get this from Eclipse here:
https://www.eclipse.org/mat/downloads.php

We'll use this tool to open a heap dump file and look at the contents.





Next Steps

Thank you for working through this course. You may be wondering what's next. Now that you have finished and this lesson, we will answer some of your questions.

{"mode":"full","isActive":false}


<details>
  <summary>Click here to view the different technologies.</summary><br>
</details>