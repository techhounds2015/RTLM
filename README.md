# RTLM

prerequisites

Operating System --Windows 8.1 Professional
 		 Windows 2012 Standard
RAM -4GB
JDK 1.7
Steps to install Logstash ,Kibana and Elasticsearch.
1)use the below links to download the softwares.

 Elasticsearch: https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.4.4.zip
 Logstash: https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.zip
 Kibana: https://download.elasticsearch.org/kibana/kibana/kibana-4.0.0-windows.zip

2)Create a folder (with your application name) under c drive and extract all the folders there.

it should looks like below.
c:\(application name)\elasticsearch
c:\(application name)\kibana
c:\(application name)\logstash
3)Add JAVA_HOME to environment variables.
4)Download logstash config file from the below URL.
Logstash.conf: https://raw.githubusercontent.com/sbagmeijer/ulyaoth/master/guides/logstash/windows/logstash.conf

place the above file in the C:\(application name)\logstash\bin

5)Install Microsoft Web Platform Installer 5.0 to run kibana as a IIS service.
6)Insall Micrisoft WebPlatform Installer5.0
download the file called "wpilauncher.exe" from the below URL
http://www.microsoft.com/web/downloads/platform.aspx

after downloading simply click it and at one point you come at a Window with applications and you "Add" 
button on the right. In the top is a search window, search here for Application Request Routing.
7)Once ARR installation completed ,Open IIS Manager and stop the "Default WebSite" and stop the service.
8)Create a new website for Kibana 
Right click on "sites" in the left part of IIS Manager and click "Add Website".
9)Create a reverse proxy in IIS to Kibana.
10)Start elasticsearch and put it on autostart
 Open a console and go to "c:\ulyaoth\elasticsearch\bin\"
now type the following command: service install
Now type the following:service manager
11)To make sure elastic search is up and running
type http://127.0.0.1:9200 and you should see JSON format.
12)Create a Logstash startup bat file
"run.bat" should simply contain this line:
Code:
logstash.bat agent -f logstash.conf
Now place your "run.bat" in the folder: C:\ulyaoth\logstash\bin

13)Start Logstash & Autostart it
Once you have the zip file simply unzip it and copy the file from the unzipped folder you now have: "nssm-2.24\win64" (nssm.exe) to "C:\ulyaoth\logstash\bin" so it should result in you having "C:\ulyaoth\logstash\bin\nssm.exe".

Now open a Command Prompt and type:


Code:
cd C:\ulyaoth\logstash\bin

And then type the following:


Code:
nssm install logstash

You will now see a GUI to create a server fill in the following:
Path: C:\ulyaoth\logstash\bin\run.bat
 Startup directory: C:\ulyaoth\logstash\bin
14)previous step you downloaded "nnsm.exe" you will need to copy the same file once more but this time copy it to: "C:\ulyaoth\kibana\bin\nssm.exe"

Now open a Command Prompt and type:


Code:
cd C:\ulyaoth\kibana\bin

And then type the following:


Code:
nssm install kibana

You will now see a GUI to create a server fill in the following:
Path: C:\ulyaoth\kibana\bin\kibana.bat
 Startup directory: C:\ulyaoth\kibana\bin
15)If you wish to adjust the settings of Kibana such as running it on a different port or IP simply go to "C:\ulyaoth\kibana\config\kibana.yml" and play around with the available settings.
16)If you did everything correct then Kibana should be running so lets test it by going to "http://(your site name)/" or the website name you did choose and you should see that Kibana is started





