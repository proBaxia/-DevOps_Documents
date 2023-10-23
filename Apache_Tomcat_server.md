+++++++++++++++++++++
Apache Tomecat server
+++++++++++++++++++++
=> Apache Tomcat is a web Server 
=> Apache Tomcat is used to run java APPlications
=> Apache Tomcat is free & open source 
=> Apache Tomcat runs on 8080 port bydefault (we can change that on port in server.xml file)

Apache Tomcat Folder Structure
++++++++++++++++++++++++++++++
bin  : it contains commands to start and stop tomcat server 
conf : it contains configuration files 
lib  : it contains libraries (jar files)
logs : it contains server log files 
temp : Temp files will be craeted here (we can delete them)
webapps: This is called as deployment folder 
Note : we will keep war file in webapps folder deployment 

Working with Apache Tomcat in Linux
+++++++++++++++++++++++++++++++++++
-> login into AWS Management Console 
-> Create EC2 Intance (Amazon Linux AMI)
-> Connect to EC2 Instance using MobaXterm/Putty
-> install java software using below command
        $ sudo yum update -y
	$ sudo yum install java-1.8.0-openjdk -y
->Verify the version of version of java install in our machine 
        $ java version 
Note: if we have multiple java versions installed then we can switch to particular version using below command 
        $ sudo update-alternatives --config java
-> we can download apache tomcat from offcial website 
     URL : https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.82/bin/apache-tomcat-9.0.82.tar.gz
-> we can find apache tomcat urls to download in official website download page 
-> Copy the URL of tar file and execute below command in linux machine 
        $ sudo Wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.82/bin/apache-tomcat-9.0.82.tar.gz
-> After tomcat tar file got download then extract Tomcat file using below command 
       $ tar -xvf apache-tomcat-9.0.82.tar.gz

-> GO inside toncat folder and see folderr structure
        $ cd apache-tomcat-9.0.82 
        $ ls -ltr

-> Go to tomcat bin directory and run tomcat server
        $ cd bin 
	$ ./startup.sh

Note: Tomcat Server runs on port by defaulf . Enable this port 8080 in your instance  Security group as custom tcp 
 * Type: Custom TCP
 * Protoal : TCP
 * Port Range: 8080
 * Source Custom (0.0.0.0/0)

 -> Access Tomcat Server from your broswer 
      URL : http://EC2-VM-Public-IP:8080/

Note: it should open tomcat server home page.

-----------------------------------------------------------------------------------------------------------------------

-> by defaulf the Host Manager is only accessible from a browers running on the same machine as Tomcat. if you wish to modify this restriction, you'll need to edit the Host Manger's context.xml file.
-> File Location : <apache-tomcat-9.0.82> cd /webapp/manager/META-INF/context.xml

-> In Manager context.xml file, change <Value> section like below (allow attribute value change)
   <Context anitResourceLocking="false"privileged="true" >
       <Value ClassName="org.apache.catalina.valves.RemoteAddrValve"allow=".*" />
    </context>

Add tomcat users in <apache-tomcat-9.0.82>/conf/tomcat-user.xml file like below   
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<role rolename="manager-gui"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>
<role rolename="admin-gui"/>
<user username="tomcat" password="s3cret" roles="admin-gui"/>

-> Stop the tomcat server "./shutdowm.sh"and start it "./startup.sh"

-> once Tomcat, Server We can access Tomcat Server admin console using EC2 instance Public IP 

-> Click on Host manager to deploy the application (it will ask for credentials, enter the credentials we have configure in "tomcatxml" file) 

-> After Login Success we can see below List of Applications Running in Tomcat 

-> Go to maven web application and package that application as war file (war file will be created in target folder)

-> we can deploy Maven Web Application 'war' into Tomcat Server from Host Manager Console 

-> Choose War file and click on 'Deploy' button 

-> you will see your application which got deployed in Tomcat Server 

-> Click on Application name it will open your War file Application on your Browser user interface