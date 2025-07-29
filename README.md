some important cmds:- 
- echo - displays message
- whoami - tells about the username
- ls - provide the list of elements in the current directory
- pwd - it tells the location for the present working directory
- cd - change directory
- cat - this is used to read inside content of the file.


Jenkins: ci/ cd  -> Continuous Integration and continuous delivery, ssh -> secure shell 
Jenkins is an automation platform that allows you automate platform via build, test and deploy the platform. 
consists of two main components: 
-Master Server
	-control pipelines
	-schedule builds
-Agents/ Minions
	-Perform the build

 -how to create a user on jenkins ?
 jenkins -> Manage jenkins -> Mange user -> create new user 
 like so you can create a new user in jenkins easily.

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

- Jenkins Role base Access Control (RBAC):
  According to this the another user can config your work after login into your pipeline.
  Even your system message and job that are done by another user remains visible.

- how to config the Role base access control ?
  There is no direct way to config the role base control for that you need to install a plugin that will help to control the role base settings for another user i.e. perms for another user. for example: another user can only build the item but can't change the configuration for that item. There are mutiple things that a new user in the pipeline can i.e they can have the read perm 
	- download the Role base authorization plugIN
   	- go to configure global settings -> authorization -> select role base strategy -> Apply and save.

- how to manage and assign roles on jenkins ?
  Configure jenkins -> security -> Manage and assign roles -> Manage Roles
  for example: developer role
  I have created a role as developer and now I want to assign it to one of the user on jenkins how can i do so ?
  
  Configure jenkins -> security -> Manage and assign roles -> Manage Roles
  cd ..
  configure jenkins -> security -> Manage and assign roles -> Assign Role
  In Assign role you can clearly see the user that are currently in the pipeline
  click on the user you want to provide the perms. then Apply and save. 
  
