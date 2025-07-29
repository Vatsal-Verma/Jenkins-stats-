some important cmds:- 
- echo - displays message
- whoami - tells about the username
- ls - provide the list of elements in the current directory
- pwd - it tells the location for the present working directory
- cd - change directory
- 


Jenkins: ci/ cd  -> Continuous Integration and continuous delivery, ssh -> secure shell 
Jenkins is an automation platform that allows you automate platform via build, test and deploy the platform. 
consists of two main components: 
-Master Server
	-control pipelines
	-schedule builds
-Agents/ Minions
	-Perform the build

 - how to create a job ?
	- go to create new item:
 	- click on the type of project you need to create.
  	- for example - freestyle project etc.
	- when the job is created then you can configure it by prodiving the cmds in my case i gave the shell cmds
   ```
   echo hello world
   ```
   output for the same:-

   ```
   hello world
   ```
- How to change the UI of jenkins ?
  The ui of jenkins can be changed with the help of plugins:
  for example the Simple UI jenkins plugin. In order to apply the ui plugins you need to config the system manager where you need to apply the url for css under the Theme platte

