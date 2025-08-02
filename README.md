# Jenkins

# some important linux cmds:
- echo - displays message
- whoami - tells about the username
- ls - provide the list of elements in the current directory
- pwd - it tells the location for the present working directory
- cd - change directory
- cat - this is used to read inside content of the file.
- ping - this is used to check for the internet compatibility.
  ```
  for example: ping 8.8.8.8
        Pinging 8.8.8.8 with 32 bytes of data:
	Reply from 8.8.8.8: bytes=32 time=9ms TTL=119
	Reply from 8.8.8.8: bytes=32 time=9ms TTL=119
	Reply from 8.8.8.8: bytes=32 time=7ms TTL=119
	Reply from 8.8.8.8: bytes=32 time=7ms TTL=119
	
	Ping statistics for 8.8.8.8:
	    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
	Approximate round trip times in milli-seconds:
	    Minimum = 7ms, Maximum = 9ms, Average = 8ms


  ```
- curl - this command is uesed to send the data to or from the server. 
- sleep - this command is used to bring a delay before each job i.e. 5 sec delay or 10 sec delay.


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

 # how to create a job ?
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
# How to change the UI of jenkins ?
  The ui of jenkins can be changed with the help of plugins:
  for example the Simple UI jenkins plugin. In order to apply the ui plugins you need to config the system manager where you need to apply the url for css under the Theme platte

# Jenkins Role base Access Control (RBAC):
  According to this the another user can config your work after login into your pipeline.
  Even your system message and job that are done by another user remains visible.

# how to config the Role base access control ?
  There is no direct way to config the role base control for that you need to install a plugin that will help to control the role base settings for another user i.e. perms for another user. for example: another user can only build the item but can't change the configuration for that item. There are mutiple things that a new user in the pipeline can i.e they can have the read perm 
	- download the Role base authorization plugIN
   	- go to configure global settings -> authorization -> select role base strategy -> Apply and save.

# how to manage and assign roles on jenkins ?
  Configure jenkins -> security -> Manage and assign roles -> Manage Roles
  for example: developer role
  I have created a role as developer and now I want to assign it to one of the user on jenkins how can i do so ?
  
  Configure jenkins -> security -> Manage and assign roles -> Manage Roles
  cd ..
  configure jenkins -> security -> Manage and assign roles -> Assign Role
  In Assign role you can clearly see the user that are currently in the pipeline
  click on the user you want to provide the perms. then Apply and save. 


  # how to build the jenkins test without manual building ? 
  - This can be done by configuring the authentication token which can trigger the build remotely.
  - steps:
    	- go to project configuration then under the title "Build Trigger" hit build trigger remotely.
    	- Then It will provide you the authenication token which you will concatenate with the token uri
    	for example: you jenkins runs on server http://localhost:8080/

    ```
    LOCAL_HOST/job/test-token/build?token=TOKEN_NAME
    http://localhost:8080/job/test-token/build?token=TOKEN_NAME
    ```

  
    - problem in this:
      The main problem which is occuring because of the build trigger is that we are not able to run/ Build the test on the prompt or shell
      and return the authentication error:-

      fix: use Build authentication token root (plugin)
      here the url changes a litle bit, but with this method you can build your job easily without any authentication failure.

      ```
      ${localhost_url}/buildByToken/build?job=RevolutionTest&token=${token_name}
      http://localhost:8080/buildByToken/build?job=test-token&token={}
      
      ```
      you can also do this with the help of you sh terminal without any authentication error.
      you can just pass the uri which is created after using the Build authentication root plugin that you need to pass with the curl in sh.

      ```
      curl http://localhost:8080/buildByToken/build?job=test-token&token={}
      ```

      problem: This cmmd won't work as it is. This is because of the '&' special character.
      fix: you need to replace '&' with '\&' in order to fix this problem.
      ```
      curl http://localhost:8080/buildByToken/build?job=test-token\&token={}
      ```
# Jenkins upstream and downstream 

  upstream is used to build a job before the current job is build. 
  downstream is used to build a job after the current job is build. 

  when to use this?
  this is used when a parent job require to trigger the child job to perform some functionality. 
  
  To do so you need to do as follow:-
  jenkins configure -> Build Trigger -> mark check on the Build after other projects are built -> write your project name that you want to trigger before or after the current project -> Then mark check on build    only if the previous or ahead build is stable. 

  There are other options too: 
  1) build even if the the previous build is faild
  2) build even if the previous build is unstable

# Build trigger periodically
  This allows you to trigger a job periodically. In this you are required to follow the cron based sytnax. To know more about the cron syntax please refer this [link](https://crontab.guru/)
  for example: 

  ```
   H/2 * * * *
   This will trigger the build after every 2 mins gaps. 
  ```

# 

# Poll SCM (Source Code Management)
  Poll SCM is another technique which is used to trigger the build. If there is any change in the base code then this build will be trigger immediately. 
  for example:

  ```
  H/2 * * * *
  This will check for the change in the code base in every two minutes. If it find any change in the code base then it triggers the build.
  ```

# Environment Variables: 
  When you execute a build or a shell then some hidden commands are executed automatically along with it which are environment variables. for exmaple: BUILD_URL etc.
  you can check that as follow, run the shell command as follow:

  ```
  echo "${JOB_NAME}"
  echo "${BUILD_ID}"
  ```
# Parameterized jobs in Jenkins
  This type of job allows the user to input during the build. For doing so, you need to config the project. Go to project -> configure -> mark select on "This project is parameterized" -> add parameters -> 	      (configure the name of variable, it's default value if required and description if required) -> Then you'll see that whenever you build a project then the button says "build now" and after configuring the        project it says "build with parameters". 

  The parameter can be a String, boolean, Integer, Password, multiLineString params etc. You need to enter these params before the job is build. To Verify if the params are set you need to do as follow: 

  ```
  echo "${String_param_name}"
  echo "${boolean_param_name}"
  echo "${multiLinedString_param_name}"
  echo "${password_param_name}"
  ```

# Abort Build
  According to this if the build takes more than the set time, then it aborts itself if that happens. In order to config this you need to locate as follow: jenkins job -> configure -> under Build environment       section -> click mark on "Abort Build If Stuck". if set-time < actual time taken, then the build aborts. 
  for example: I have set time as 2 mins and I let the build sleep for 240 seconds which is 4 mins then it fails. 

  ```
  sleep 240 
  ```
# Add TimeStamp to the console output
  With this function enabled you can get to know at what time what function occured. It simply shows you the actual time of execution of each step in your console output. 
  In order to config this you need to locate as follow: jenkins job -> configure -> under Build environment section -> click mark on "Add Timestamp to the console output"
  for example: 

  ```
  19:31:19 + echo 'My name is vatsal'
  19:31:19 My name is vatsal 
  19:31:19 + echo 'I'\''m a student: true'
  19:31:19 I'm a student: true
  19:31:19 + echo 'I'\''m 12 years old.' 
  19:31:19 I'm 12 years old.
  19:31:19 + cat filename
  19:31:19 Finished: SUCCESS
  ```
  
  
