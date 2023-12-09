### youtube 
* Configuration panale 
* Build queue
* Build executer status panale
* u want to see users then __people__ option
* My view u have multiple jobs and u want to  see difreant views then use  __my view__
* New View want to create new view
* Search bar u can use as a navigation bar u want to search the build with num and last faild build or last success build or last stable or last unsuccessfull build may thing && u want to go any configure system or manage plugins like that 

### manage jenkins 

* configure system
  * any pulgin installed and u want to change any plugin related configuration
* Global Tool Configuration
  * any tool configure
* manage plugin
  * add remove any plugin
* configure global security
  * give user to sing or not access jenkins or not
* manage credential
  * u can store the credentials and u can use them in jobs
* manage users
  * u want add or remove the user and modifi the user that can loginto jenkins
* download __role based  authorization strategy__ this plugin is use for when u create the user the user can access any ones project and they can do any thing for that we have to install this plugin __role based  authorization strategy -> configure globale security -> in authorization select the role based strategy__ then u will see the option in manage jenkins manage role and assign roles
* manage jenkins -> manage and assign roles -> role to add -> role name <developer>  and select the options 	 then  __Assigen Role__  -> user/group to add and user name <rizwan>  -> select the permission developer
* we  have multiple user and we want to give permission to specicific project for that we need go manage jenkins -> security -> authorization (project based matrix autharization strategy ->  then we have to add user and select the specifi role to them like read update or delete -> overall , credentials , agent , job , run , view, scm then go to specfic prject  -> enable project-based security  then u can select the option read build like that 
* we have  A-team and B-team we want to give access to A-project to A-team and B-project to B-team for that we have to use -> manage jenkins -> security -> authorization (project based martrix autharization startegy > then u have to add group A_team and B_team then give the access like read or delete many thing ->

#### jenkins job

##### Source Code Management
  * we have to download plugin then it will show that plugin option and u have to select that plugin

###### Build Triggers
* when u Build the job u have to doit maually but there is option like Build Triggers without manual intervention
* __Trigger builds remotely (e.g from scripts)__
  * Use the following URL to trigger build remotely: JENKINS_URL/job/demo-4/build?token=TOKEN_NAME or /buildWithParameters?token=TOKEN_NAME
  * http://localhost:8080///job/demo-4/build?token=myjob
  * if u want to execute the jenkins job with the help of shell script u can use __Trigger builds remotely (e.g from scripts)__
  * when we try to trigger job from terminal with URL?token=TOKEN_NAME we get error like authentication Token error to resolove this we need to download the plugin
  * plugin jenkins __Build Authorization Token Root__ install this plugin
  * then u have to search the jenkins plugins in that __Build Authorization Token Root__ u will find token url how to call from curl  or browser
  * buildByToken/build?job=RevolutionTest&token=TacoTuesday modifi with job name and token __http://localhost:8080/buildByToken/build?job=demo-4&token=myjob__
  *  if u want  to  call from terminal u have to use \& __http://localhost:8080/buildByToken/build?job=demo-4\&token=myjob__
* __Build after other project are built__
  * we have job for git clone another one bulid another one deploy once clone is complete then build job will trigger once build job success then deploy job will trigger 
  * in this we have multiple options like build stable or unstable or build fails or build aborted
  * unstable advane -> exit code to set build unstable -> in shell script exit 10 if u get exit code more than 10 declare unstable  
  * we can choose multiple jobs if multiple any one job success it will trigger this job
  * up-stream job before this job trrigers that job will run then this job will triger
  * down-stream job after this job after this jobs run then other job will trigger __H/2****__
###### Build periodically
  * if u want to run job every 2 mints like then we can use this trigger 
###### GitHub hook trigger for GITScm polling
  * if any thing happen in SCM like code commit or push like then it will trigger the job with help of hooks concept in git there is concept like git webhooks 
###### Poll SCM 
  * Poll SCM use any SCM link like git then __H/2****__ it will check the every 2 mints SCM repository if there is any new code it will trigger the job if there is no new code it will not trigger any job

 
* 11. in jenkins delete workspace before build starts  it will clear the workspace before build starts and u can select the advance option for delete the particular pattren files and directory 

###### Environment Variable

```
name=Basha
echo "hello my name is ${name}"
```
* by default jenkins give some Environment Variables u can see them jobs -> select the job -> build -> see the list of avilable environmet variables (BUILD_NUMBER, BRANCH_NAME, TAG_DATE, BUILD_ID ETC.....)

```
# name=Basha
# echo "hello my name is ${name}"

echo "demo-ENV build number is = ${BUILD_NUMBER}"
# ${BUILD_NUMBER} its a default jenkins Environment Variable
```
* when u build ur job u will get some artifacts u have to store those artifacts into some repository u have multiple artifacts its dificult to find which artifats for that u can use ENV __BUILD_NUMBER__ it will store the artifacts with build number
* when u build code in jenkins and that code comes from git and u want to identify the commiter name for that u have jenkins ENV __GIT_COMMITTER_NAME__

###### GlOBAL VARIABLES
* u have to create Global variables wich will use in multiple jobs manage jenkins -> configure system -> global properties  -> click Envoironment variable -> Name = GLOBAL_var Value = mytestGlobalvar then u can use this GLOBAL VARIABLE in ur multiple jobs
* u have some value that requeied for multiple job without going into every job and writing and if need to be some changes in feature u dont need to go every job u can use jenkins GLOBAL VARIABLES u just change in one place it will refleact in every job where u mention that variable
* any parameter or any variable is same for multiple project and u want to use that and in feature it will change u dont need to go every project u just change in global variable place


###### USER DEFIENED VARIABLES
* The parameters that a user should provide when triggering the Pipeline.
* BUILD WITH PARAMETER
* job -> This project is parameterized  -> boolean, choice, credential, multiline string, passwdord, run, string. 

* u have run the project and that goes infinite loop and it will not come out so u loose one executer so how u can set certain time for project come out after some time like it will take too long time but we can set time if this job goes more than specific time it will abort or fail 
* __Build Environment__ -> abort the build if its stuck -> timeout minutes 

###### ENABLE/DISABLE JOB
* u dont want to build the specific job or any job becouse is there any maintaincemode for jenkins server or there is no slave servers and u dont want to run any new job or specific job for that u can go specific project up-right side u will finde option like disable and u can enable

* __Parallel build__ u have one job and u want to run mutliple times parallely by default it will build with que like first build then second build but u want to parallely so go to jobs -> click execute concurrent builds if necessary
*  __retry count__ u can give number like 3 it will try for 3 times
* __Throttle Build__ u want to build only 4 build in 1hour time time period, u cant build the job more than 4 in 1 hour time for this option u have to install plugin __Branch API Plugin__

* __WORKSPACE__ when ever u create job in jenkins it will create one workspace with job-name then u do anything like code clone build all this will store in that workspace 
* Custom Workspace __/var/lib/jenkins/workspace/job-name__
* if u want to change the default workspace to custom workspace 
* __job -> general -> use custom worspace -> give directory path__
* u have multiple jenkins servers and it mounts nfs server u want to use that mount path then use custom workspace

* __Block build when upstream project is building__  u have parent and child jobs when upstream(parent) job is running and some one try run downstream(child) job it will not run it will be in pending state once upstream job done then only downstream job will run
*  __Block build when downstream project is building__ u have parent and child jobs when downstream(child) job is running and some one try run upstream(parent) job it will not run it will be in pending state once downstream job done then only upstream job will run

* plugins 
  * maven integration
  * deploy to container
  * code pipline
  * Copy Artifact
* when u install jenkins plugin it doesnt mean that u have installed maven application u have to install maven application manually or in jenkins -> manage jenkins -> Global Tool Configuration -> maven install automatically and version
*__tomcat9__ location for war file __/var/lib/tomcat9/webapps/ROOT/__ 
* user configuration in tomcat9 __/etc/tomcat9/tomcat-users.xml__ in that u have to past like 

```
<role rolename="manger-gui"/>
<user username="tomcat" password="s3cret" roles="manager-gui,manager-script,mnager-jmx,manager-status"/>
```
* service tomcat9 restart
* __Paralell Build__ manage jenkins -> configure system -> # of executors -> 
* we run multiple jenkins jobs as a paralell build like multiple jobs at a time maybe u get running out of memory or jenkins will crash for that we have concept called __Jenkins MASTER / SLAVE__ 
* __Distrubuted Build__ when ever u run any job it will distrubeted to slave node is there any node is available and the node is helaty or not will check by master node 
* u can run any job in master also but its not gud practice 
* __ADD SLAVE NODE__ manage jenkins -> __Manage Node and Clouds__ -> new node -> name -> permanent Agent ->  # of executors -> remote root directory -> __Labels__ -> us as much as possible
* __launch agent__ for launching the agent slave node should have java 
* __sudo mkdir /var/jenkins__
* __chown basha:basha jenkins/__
* __ls -l__
* if u want to run specific job into specific Slave Node u have to use lables when we configuring slave node we give label and in our project configuration __Restric Where this project can be run__ -> lables Expression 
* why we use lables becouse we have multiple os's like windows linux many thing we have projects like some of runs only windows some of runs only linux for that we can use lables 

* why we need pipline as a code?
* when we build the pipline as a freestyle project we need to build multiple jobs like code pull, code test, code build, artifact store, deploy to deploy one project we need to build multiple project  and its very hard to maintain for that we need pipline as a code  
* we can store our pipline as a code into our code repository and we can maintain versioning 

###### Pipline as Code 
```
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

```
pipeline {
    agent any
    stages {
        stage('CODE-PULL') {
            steps {
                sh '''
                echo 'Hello World'
                sleep 10
                date
                '''
            }
        }
        stage('TEST') {
            steps {
              echo 'Hello World'
              sleep 10
            } 
        }
        stage('BUILD') {
            steps {
                echo 'Hello World'
                sleep 10
            }
        }
        stage('DEPLOY') {
            steps {
                echo 'Hello World'
                sleep 10
            }
        }
    }
}

```

* New Item -> pipline -> general 
                             * enable project-based security
                             * discard old builds
                               * when we run jobs it will generate console output and archived artifacts and any other metadata  so keeping all the jobs data will consume lot of space for that we can use __discard buids__ we can choose option like __1.Build age: discard builds when they reach certen age__ __2. Build count: discard the oldest build when certian number of builds already exist__ 
                             * do not allow concurrent builds
                               * I do not want to allow two jobs of the same type (same repository) to run in parallel on the same node.
                               * when we click build now multiple time it will build paralelly for multiple times it doesnt mean to build same job and same branch same repository run multiple times it will consume multiple executor for that we can use option like  __do not allow concurrent builds__ in pipline __diseble concurrent builds__ 
                               * when u select this option in que job#1  is completed then other  que job#2 will run 
                             * do not allow the pipline to resume if the controller restart 
                             * gitHub project 
                             * pipline speed/ durability override 
                             * preserver stashes from completed builds
                             * theis project is parameterized 
                             * throttel builds 

* __Restrat a jenkins pipline from stage__ when we runing our jobs as a pipline we have multiple stages like code pull and code build and code test and code deploy in this stages u want to rerun any stage we can any stage faild we can rerun prticulor stage 
* You can restart any completed Declarative Pipeline from any top-level stage which ran in that Pipeline. This allows you to rerun a Pipeline from a stage which failed due to transient or environmental considerations, for example. All inputs to the Pipeline will be the same. This includes SCM information, build parameters, and the contents of any stash step calls in the original Pipeline, if specified.

```
pipeline {
    agent any
    stages {
        stage('CODE-PULL') 
        stage('TEST') {
            steps {
                sh 'echo "${BUILD_ID}"' // jenkins environment

            }
        }
    }
}
```

* __user Defined Varaibales__

```
pipeline {
    agent any
    environment {
      name= 'BASHA'
    }
    stages {
        stage('CODE-PULL') {
          environment{
            name= 'basha'
          }
            steps {
                 sh 'echo "${name}"' // user-defined  environment at stage level 
                    }
                    }

        stage('TEST') {
            steps {
                sh 'echo "${name}"' // user-defined  environment

            }
        }
    }
}
```

* u can give environments at pipline level and at stage level 

* __Build with Parameter__

```
pipeline {
    agent any
    environment {
      name= 'BASHA'
    }
    parameters {
      booleanParam(name: 'ismale', defaultValue: true, description: "")
      choice(name: 'city', choices: ['jaipur','Mumbai','pune'], description: "")
      string(name: 'person', defaultValue: 'Rizwan', description: "give the ur name")
    }
    stages {
        stage('CODE-PULL') {
          environment{
            name= 'basha'
          }
            steps {
                 sh 'echo "${name}"'// user-defined  environment at stage level 
                 sh 'echo "${city}"'
                    }
                    }

        stage('TEST') {
            steps {
                sh 'echo "${name}"' // user-defined  environment

            }
        }
    }
}
```
* u can build the job with parameter 

* if u want to manual intervintion like manualy user want to give some input u can use but it stage level only 
* user want to continue the stage they can use __input__ option 

```
pipeline {
    agent any
    environment {
      name= 'BASHA'
    }
    stages {
        stage('CODE-PULL') {
          environment{
            name= 'basha'
          }
            steps {
                 sh 'echo "${name}"' // user-defined  environment at stage level 
                    }
                    }

        stage('Contuine or abort') {
            input {
              message "should we continue?"
              ok "yes we should"
            }
            steps {
                sh 'echo "${name}"' // user-defined  environment

            }
        }
    }
}
```

* usually jenkins run every stage one after  other if any stage fails it wont run next stage but u have requrement like any stage fail dont consider always run the particulor stage for that we need to use __post__
* __post__ option we can use stage level and complete pipline level 
* if any stage fails send notification like that 
```
post {
  always {
    echo 'I will always say hello again!'
  }
  failure{
    echo 'if any stage fails'
  }
  success{
    echo 'only when pipline success if any stage aborted that time also not run this stage all pipline success then only this will run'
  }
}
```
* Some actions like sending notifications and saving logs and running other piplines 

```
pipeline {
    agent any
    environment {
      name= 'BASHA'
    }
    stages {
        stage('CODE-PULL') {
          environment{
            name= 'basha'
          }
            steps {
                 sh 'ech "${name}"' // user-defined  environment at stage level 
                    }
                    }

        stage('Contuine or abort') {
            input {
              message "should we continue?"
              ok "yes we should"
            }
            steps {
                sh 'echo "${name}"' // user-defined  environment

            }
        }
    }
post {  // post action always run if any stage fail or success it doesnt consider
  always {
    echo 'I will always say hello again!'
  }
}
}
```

47. 

* we have pipline with multiple stages like 20 stages when we run the pipline it fails 19 stage and it take 2 hours to come at 19th stage so u did some changes in pipline and u run again but it fail again so for that we dont need to run every stage beacouse it consume lot of time for that we can run only 19th stage by using __blue ocean plugin__ and __Declarative pipline__
* __blue ocean plugin__ when u run job it will show the every stage if any stage fail click on that stage there is option like restartstagename
* Scripted pipline u cant restart any stage 
* Declarative pipline u can restart any stage at any time 

* we can write jenkins pipline or pipline syntax generator or blue ocian 
* while writing jenkins file how can u mention that maven install it means maven autometically will installed by jenkins 


```
 pipline {
  agent any 
  tools{
     maven 'apache-maven-3.0.1'
  }
  stages {
    stage('example') {
      steps {
         sh 'mvn --version'
      }
    }
    }
 }
```
###### Jenkins Slack Notification
```
pipeline{
    agent any
    stages{
        stage("GIT CODE PULL"){
            steps{
                slackSend channel: 'jenkins', color: 'good', message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
                slackSend channel: 'jenkins', color: 'good', message: "GIT CODE PULL STAGE STARTED"
                echo "========GIT CODE PULL====="
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("CODE TEST"){
            steps{
                echo "========CODE TEST====="
                slackSend channel: 'jenkins', color: 'good', message: "CODE TESTING STARTED"
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("CODE BUILD"){
            steps{
                echo "========CODE BUILD====="
                slackSend channel: 'jenkins', color: 'good', message: "CODE BUILDING"
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("CODE DEPLOY"){
            steps{
                echo "========CODE DEPLOY====="
                slackSend channel: 'jenkins', color: 'good', message: "CODE DEPLOYING"
                // for deploying on container we need to install deploy on container plugin 
                deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://192.168.0.1:8080')], contextPath: 'app', war: '**/*.war'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"``
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
```

```
   stages{
    stage('helo') {
        when {
          equals expected: 3, actual: 'b'
          // if expt and actu are not matching this stage will skiped
        }
      }
    stage('helo') {
        when {
          equals expected: '3', actual: env.BUILD_ID
          // when we use env varibles we need to use '3' beacouse string 
        }
      }
    }
```
* when u want to skip or do something in jenkins pipline we can use __tag__ option 
* we have multiple environments and we want to deploy our application in diffreant environment for that we can use jenkins pipline in that we can use tags like when tag if dev this stage will run when tag if stage is qa this stage will run  

```
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'make package'
            }
        }
        stage('Test') {
            steps {
                sh 'make check'
            }
        }
        stage('Deploy') {
            when { tag "release-*" } 
            // This means the stage would only execute when the Pipeline has been triggered from a tag in Git matching the release-* Ant-style wildcard.
            steps {
                echo 'Deploying only because this commit is tagged...'
                sh 'make deploy'
            }
        }
    }
}

```


* CAN we have multiple agents in jenins pipline ?
* yes we can run multiple agents 
* we can run agents at pipline level or every stage level
* we can have multiple labels for single agent 
* in jenkins pipline we can use condition like

__agent { label 'node1 || node2' }__ job will run node1 or node2 wich ever node is available 
__agent { label 'node1 && node2' }__  it will node1 and node2 who has lable like that if any node dosnt have this cobination job will start but never finished  [nodelabel node1 node2] we can give single node to multiple labels 

```
pipeline{
    agent none

    stages{
        stage("A"){
            agent { label 'node1'}
            steps{
                echo "========executing A========"
            }
        }        
        stage("b"){
            agent { label 'node2'}
            steps{
                echo "========executing b========"
            }
        }
    }
}

```

* __NODE LABEL__ if u doesnt want to use default workspace u want to use custom workspace then u can use __NodeLabel__

```
pipline 
  agent {
    node {
      label 'node1'
      customWorkspace '/home/basha/my-custom-workspace'
    }
  }
```
* what is meaning of agent any?
* it means any agent availbel 
* first time it runs in node1 and u run other time it will run same node1 becouse it remember the whre first job runs its run same node until same node goes offline

* how to disconnect agent ? 
* we have multiple jenkins nodes and some of node we want to put in maintains mode like any update that kind of thing for that we need to disconnect 
* manage jenkins -> nodes -> select node -> Disconnect -> markthis node temporarily offline  once done MM 
* select the node -> bring this node online -> launch the agent 
* if doenst mark this temporarily offline when u refresh or restart it will come to online 

* Retain Builds Forever?
* currentBuild.keepLog = true
          // it will keep the build forever it diseble delete build '#2'

```
pipline {
  agent any
  stages{
    stage('hello') {
      steps{
        script {
          currentBuild.keepLog = true
          // it will keep the build forever it diseble delete build '#2'
        }
      }
    }
  }
}
```

* Resume jenkins job in jenkins when we run the job if any stage jenkins server restarted job will be resume where ever its stoped 

* Run Different steps in jenkins pipline based on branch 
* we have multiple branch in git and we want to run our jenkins job for every stage for particulor branch

```
pipline {
  agent any
  stages {
    stage('for main branch') {
      when {
        branch 'main'
      }
      steps{
        echo 'main branch'
      }
  }
  stage('for stage branch'){
    when {
        branch 'stage'
    }
    steps {
        echo 'stage branch'
    }
  }
  stage('for pull request') {
    when {
        changeRequest()
    }
    steps {
        echo 'pull request'
    }
  }
}
}
```
* how to change jenkins folder 

```
pipeline{
    agent any
    stages{
        stage('full path'){
            steps{
                sh 'cat my-project/file.txt'
            }
        }
        stage {
            steps {
                dir('my-project'){
                    sh 'cat file.txt '
                }
            }
         }
        } 
       }
```
* how to change jenkins port?
* ps -a 
* systemctl edit jenkins
* __cd /usr/lib/systemd/system/__
* __ls *jenkins*__
* __sudo vi jenkins.service__

* how to reset jenkins admin passsword?
* __systemctl stop jenkins__
* __cd /var/lib/jenkins/__
* __vi config.xml__ 
* __<useSecurity>true</useSecurity>__ to __<useSecurity>false</useSecurity>__  take backup before making any changes in this file 
* __systemctl start jenkins__
* manage jenkins -> configure global security -> security Realm -> none to jenkins own user database -> allow user to sign up? uncheck 
* goto people admin -> configure -> password new password 
* manage jenkins -> configure global security -> anyone can do anythoing to logged-in user can do anything -> uncheck allow anonymous read access?

* trigger the job (downstream job)

```
pipline {
  agent any
  stages {
    stage('hello') {
      steps {
        echo 'hello friends'
      }
    }
    stage('trigger job2) {
      steps {
        build 'job2'
      }
    }
  }
}
```
* jenkins some jobs are running and that time i want to restart the jenkins server ther is a option like __/restart__ or __/safeRestart__  
* __/restart__ imidiatly it will restart the jenkins 
* __/safeRestart__ it will wait to finish the jobs which are running once all jobs are completed then only it will restart 

* discard old build in pipline
```
pipline {
  agent any
  options {
     buildDiscarder logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '', numToKeepStr: '3')
}
  stages {
    stage('hello') {
      steps {
        echo 'hello friends'
      }
    }
  }
}
```

* when we pull the code from git jenkins default checkout scm u dont need to specifi that u can also do __skipDefaultCheckout true__ 

* __Throttle__ when we run the job we want to wait to trigger other job like once the job is completed and wait for 1 minute to trigger next job  
* 

* how to increase git clone timeout in jenkins pipline?

* what is diffreance between scripted vs declarative pipline?

* when u use declarative pipline by default it will checkout SCM  but scripted not 
* when u using declarative u get  a option like restart from stage  (restart from stage means u have 10 stages and u want to start ur job stage5 it will skip the 1,2,3,4 stage it will start from 5th stage)
* when u use scripted there is no restart from stage 

* how to use jenkins lockable resources?
* when we run the jenkins job multiple time it run job when u use lockable resources it will wait complete the job1 once job1 is completed then job2 will run  but we can get this option in throttel in throttel there is quit period it will wait some time in betweent the jobs once job1 is completed it will wait some seconds then run job2 
* lockable resources u need to install plugin and  -> manage jenkins -> configuration -> lockable resources -> name  my-unique-resource -> description -> Labels agent1 -> reserved by (when we doing some sort of maintains for that no job will run for that u have to reserve once done maintance )

```
pipline {
  agent any 
  stages {
    stage('hello') {
      steps {
        lock('my-unique-resource') { // configuration -> lockable resources name -> my-unique-resource          sh 'echo hello world'
          sleep 60
        }
      }
    }
  }
}
```

* deleteDir() it will delete the current directory and its content  in that files 

* Parallel pipline 

```
pipeline{
    agent none
    stages {
        stage('BuildandTest') {
            parallel {
                stage('macos') {
                    agent {label 'macos'}
                    stages {
                        stage('Build') {
                            steps{
                                sh 'echo do build for macos'
                            }
                        }
                        stage('Test'){
                            steps {
                                sh 'echo do test for macos'
                            }
                        }
                    }
                }
                stage('linux') {
                    agent {label 'linux'}
                    stages {
                        stage('Build') {
                            steps {
                                sh 'echo do build for linux'
                            }                        
                            }
                        stage('Test') {
                           steps {
                            sh 'echo do test for linux'
                           }
                        }
                    }
                }
            }
        }
    }
}
```
* we have  mulitple nodes and we want to run our jenkins pipline as a paralelly into 2 nodes in paralelly like 
macos build and test deploy 
linux build and test deploy 

![jenkins paralell-1](./images/jenkins paralell.png)

* jenkins backup 

* how to safely upgrade jenkins to a new version?
* install plugin __support-core__   

* schedule a jenkins job to run evry hour?

```
pipline {
  agent any
  triggers {
    cron '* * * * *'
  }
  stages {
    stage('hello') {
      steps {
        sh 'echo hello world'
      }
    }
  }
}
```
* when ever u create job first time u need to manually trigger the job then only it will run every time 

* git Support for password authentication was removed on aug 13 2021 use personal access token instead.
* settings -> developer settings -> personal access tokens -> select options generate token -> copy token -> in jenkins add credentials -> username [mail.com] -> password -> id -> add 

* in jenkins we can make our success job to as failure using __currentBuild.result = 'FAILURE'__


```
post {
  success {
    script {
      currentBuild.result = 'FAILURE'
    }
  }
  }
```
07-12-2023

* how to setup docker container as build agents for jenkins
* install plugin __docker pipline__ 

```
pipline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
```

* when u use docker image as a jenkins agent it will look is there any docker image u called if any image is not present in local it will pull form public repository and create a container and will perform all stages once completed it will stop the container and remove the container 
* we can use docker container as a jenkins node at globale level or every stage level 
