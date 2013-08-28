# jmxmon

  jmxmon is a tool for monitoring your Tomcat servers and the JVMs upon which they run. 
A very small, minimal webapp is created that will run on your Tomcat server. From there, jmxmon will collect JVM and Tomcat metrics using JMX, and push the results to CopperEgg.
jmxmon is built upon the open source embedded-jmxtrans code.

  This monitor does not need to be compiled with your Tomcat app. To install, you simply edit one file, build the jmxmon webapp, and copy it to your tomcat/webapps directory.

# Setting up to build your jmxmon

### 1. Check your installed version of maven  
  
```xml
mvn -version
```
  
If your maven version is 2.21 or higher, skip to step 3.   
  
### 2. Install maven  
  
#### On Centos or Amazon Linux  
  
This example assume that you will be extracting maven-3.0.5 to /usr/local/apache-maven/apache-maven-3.0.5.
  
cd /usr/local/apache-maven  
  
wget http://apache.tradebit.com/pub/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz  
  
tar xvf apache-maven-3.0.5-bin.tar.gz  
  
Add some env variables to your ~/.bashrc file  
  
export M2_HOME=/usr/local/apache-maven/apache-maven-3.0.5  
export M2=$M2_HOME/bin   
export PATH=$M2:$PATH   
  
Verify everything is working with the following command  

 mvn -version  

### 3. Clone this GitHub repo:

```xml
git clone https://github.com/CopperEgg/jmxtrans-samples.git
```

### 4. Edit the jmxtrans.json file to add your Username and CopperEgg APIKey  
  
```xml
cd  jmxmon/src/main/resources
edit jmxtrans.json
    In the "OutputWriters" array, find the CopperEggWriter settings.
        Replace  <YOUR_USER_NAME>  with your user name
        Replace  <YOUR_APIKEY> with your CopperEgg APIKEY
Save and close jmxtrans.json
```  
  
### 5. Optionally, edit copperegg_config.json:

This is only recommended if you are familiar with the CopperEgg API. It isn't necessary to get started.

copperegg_config.json will create several metric groups, designed for optimal efficiency when running with embedded-jmxtrans.
It will also create 2 dashboards:
 * jvm_dashboard  
 * tomcat_dashboard  
 

### 6. Build your configured jmxmon .war file

This step is actually more 'packaging' than 'building.' It packages up the configuration files in jmxmon, including those that you edited, and creates a .war file.
  
```xml
cd jmxmon
mvn install dependency:go-offline
```
  
# Deploy jmxmon on your tomcat servers

NOTE: If you have many tomcat servers, each running the same OS, java version and tomcat version, you only need to package jmxmon one time (on an identical system).
To be on the safe side, if you are running different OS's, jvm's and/or tomcat versions, you should package jmxmon on one of each. 

### Install and start your new jmxmon 

Copy jmxmon-X.X.war to your Tomcat webapps directory.

```xml
cp jmxmon/target/jmxmon-1.0.war $CATALINA_HOME/webapps/
```

If Tomcat is not already started, start it up.
You should begin seeing metrics from your tomcat servers and jvms within a minute or so.


For documentation about the embedded-jmxtrans module, (which is pulled-in to jmxmon by maven), refer to:
* [Documentation](https://github.com/jmxtrans/embedded-jmxtrans/wiki)
* [Latest javadocs](http://jmxtrans.github.com/embedded-jmxtrans/apidocs/)

To learn more about CopperEgg, and to sign up for a free trial: 
* [CopperEgg Homepage](http://www.copperegg.com)
* [CopperEgg Signup](https://app.copperegg.com/signup)
* [CopperEgg Login](https://app.copperegg.com/login)


License
==================

Please refer to the LICENSE and NOTIFICATION files included by the authors of embedded-jmxtrans and embedded-jmxtrans-samples.

CopperEgg has provided two JSON files in this repository, which are used to configure the CopperEggWriter. 
These files are made available under the terms of the MIT License:

Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the "Software"),
to deal in the Software without restriction, including without
limitation the rights to use, copy, modify, merge, publish, distribute,
sublicense, and/or sell copies of the Software, and to permit persons
to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL
THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

