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
* we  have multiple user and we want to give permission to specicific project for that we need go manage jenkins -> security -> authorization (project based matrix autharization strategy ->  then we have to add user and select the specifi role to them like read update or delete -> )overall , credentials , agent , job , run , view, scm then go to specfic prject  -> enable project-based security  then u can select the option read build like that 
* we have  A-team and B-team we want to give access to A-project to A-team and B-project to B-team for that we have to use -> manage jenkins -> security -> authorization (project based martrix autharization startegy > then u have to add group A_team and B_team then give the access like read or delete many thing ->)

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

![jenkins-paralell](./images/jenkins%20paralell-1.PNG)

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

================================================================================================================================================

#### DEVOPS

![devopscicd](./images/devopscicd.PNG)

![devopscicd1](./images/devopscicd1.PNG)

##### DevOps Lifecycle

![devopscicd2](./images/devopscicd2.PNG)


* What is The Version Control System?
* A system that keeps records of your changes ur doing any changes to ur code it is tracking/record  those changes 
* if u use VCS its allows to u know who made what changes & when 
* Allows u to rever any changes 
* __Version Control System Types__
* __Local__
  * local computer its record what changes have made by me and when and it alway point to latest changes if u want to go back previous u can go 
  * __Local Version Control System__ works if u are a single developer or u dont want to colabrate team 
* __Centralized Version Control System__
  * CVCS u have centralized repository  or main server repository and collaborator and developers communicate with main server repository 
  * u dont have any local copi of ur code in centralized repository 
  * in case centralized repository not accessble developer could not write the code becouse Centralized repository alway accessble 
  * centralized repository is sloves the problem to work with group of people if any case centralied repository is not accessble it is a problem for developer or colbarator
* __Distributed Version Control System__
  * widly use this DVCS it has main server repository and local repository like what ever code having in main repository same available in local repository u can sysnc local and main and developer continue to write the code if main repository goes down becouse same code available in local repository 
  * before pusing ur code remote u have to push local repository and if u dont have local and remote repository other colabrator can have same code  they can push code from there local to main server repository from there everybody in team can access the code 
  

![devopscicd3](./images/devopscicd3.PNG)

* git config --list (it will list all the  git configuration) 
* how to become folder as a git repository using __git init .__

![devopscicd4](./images/devopscicd4.PNG)

![devopscicd5](./images/devopscicd5.PNG)
 
* __git diff__ it will show the changes between working area and staging area a stand for working area  b stands for staging area 
* to compare staging  area to local repository __git diff --staged__ 
* __git diff HEAD__ it will compare with working area with local repository 

![devopscicd6](./images/devopscicd6.PNG)

* __git diff 2342fd3 24fef33__ u want to compare with 2 commits difreance between 2 commits 

![devopscicd7](./images/devopscicd7.PNG)

![devopscicd8](./images/devopscicd8.PNG)

* __git clone__ if repository not exists in ur system then we need to use __git clone__
* __git pull__ repository already available and few changes u want to pull from remote repository 

* __Connecting to github using SSH__
* generate the ssh key 

* __ssh-keygen__
* __cd /root/.ssh__  copy __id_rsa/pub__ on to github account 
* __eval $(ssh-agent -5)__
* __ssh-add ~/.ssh/id_rsa__ add ssh private key to agent 

* if u wan to see diffreance betweent 2 commits __git diff 3fafcf3 ff32rfdf__ 
* __git diff HEAD HEAD~1__ previous commits
* __git diff HEAD HEAD~2__ previous commits 
* u have writen a working application but after few commits application got currepted u dont know who has commits those bugs for that u can use __git log__ but u want to see specific file who has done the chnage 
__git annotate jenkins_dockerfile__
* if u want to identifi with git log command who has done this change then we need to got to each commit and check what files he has modified 
* if u want to go back prevoius commit we can use __git checkout commitid__
* when ever 2 developer trying to update same file and same line of code then merge confilict happen to reslove this whoever is created this merge conflict they have to sit togather and understad that wich commit should go into git repository thos commits they have to do 

* __Protected Branch__ we have multiple branches in our git repository and maste/main branch is connect to production for that we dont want to mess up with this branch like if contributer/owner  push the code into master/main branch directly if any bug we loose production for that before pushing this branches first it has to go to some reviwe process to review the code then only it should get commited again it comes as pull request  

* __Protected Branches__ github -> settings -> branches -> add Branches protection rules -> name branch -> click -> require pull request reviews before mergng(required approving reviews.3) / require status check to pass before merging / include administrators -> create 

*  __git Tags__ tags are ref's that point to specific commit in git history.
* usaly we create tag to refs to a specifi commit wich is working fine 
* working on project after doing multiple commints i have created a bug free code it has some commit id wich is not for me to remember the i tag  that as a userfrendly name so that it is for me to remember 
* tagging is generally used to capture a piont in history that is used for marked version release 
* a tag is like a branch that doesnt change 
* __git tag__ list of tags 
* __git tag v1.0__ at  this time what ever code in branch it is going to tag it as v1.0 
* __git push origin v1.0__ to push tags to remote repository 
* __git tag -a v1.1 2413rfjoi -m "version 1.1 which works with customer potal"__ 
* __git push origin v1.1__

* __REVERT CHNAGES__

![devopscicd9](./images/devopscicd9.PNG)

 __Rever changes from working directory__

```
git restore <file_name>
git checkout --<file_name>
```
* NOTE: even u can remove changes manually. but f we have update multiple files and dont know which lines to remove this command really helps 

__Rever changes form Staging area__

```
git restore --staged <file_name> # to revert canges from staging area to working directory 
git restore <file_name> # revert changes fromworking directory 
```
__Rever changes from Local Repository if u havent commited in to remote repository__

```
git reset HEAD~  # to revert chnages from local repo to working directory 
git reset HEAD^2 # two commits back 
git restore <file_name(s)>  # to rever changes from working directory
```

__Rever changes from remote repository__

we dont have direct way to do this  

__GIT REBASE__

* git rebase we use we want to squeze multiple commite into one commite like i have 5 commite i dont want to push those 5 commits into my repository the i can convert those commits into a single commit 

* __git rebase -i HEAD~4__

```
pick 3432432 added number 2 
squash wre3edf added number 3
squash rerfcee added number 4
squash wfcerfe added number 5
```
* 3 commits add into number 2
* add commit message
* git log 



![devopscicd10](./images/devopscicd10.PNG)

* __git pull__ pull the changes from remote repo to local system, if any chnages in remote repo thos get updated in our local repo at the same time the content updated in remote repo same content get pulled into local repo and working directory 
* __git featch__ it going to sync with remote repo to local repo but u cant see the changes of remote repo files in our woring directory if u wnat to get those changes into local directory again u need to execute __git merge__ command 

* __git pull__  = __git featch + git merge__


* devops engineer, can u create a repository for new project?
 
![devopscicd11](./images/devopscicd11.PNG)


![devopscicd12](./images/devopscicd12.PNG)

![devopscicd12](./images/devopscicd13.PNG)

* when ever u create git remote repository it will create default master branch if u want to delete the default master branch first u need to create onother branch and make that branch as a defaut branch then  only u will  delete master branch 

* repository -> branch -> change defult branch -> scrol down -> selecte branch -> udate 
* create protection to  branches -> branch -> branch protection rules -> add rule -> branch name pattren -> click -> require pull request reviews before merging (required approving reviews:2) -> create 

* add colaborater -> settings -> manage access -> add co

llaborater -> invaite a collaborater -> 

![devopscicd14](./images/devopscicd14.PNG)

* we have source code but we cant deploy our source into application server for that we need to compile our code then only we application system understand 


#### MAVEN
* maven can able to download the all third party libraries whcih are requered for ur application and it also do the compilation, test, even deployment of application not only this if any update in third party libreies or package whcih are u using  u just need to update that file its autometcally downloads when ever ur compiling or testing ur code 
* maven can help us build our application with all requierd packages with the minimal effort 
* sharing only source code for community or people who ever want to us ur application allong with the file wich mention that what libreis doest it requier that file we callit as __pom.xml__ 


![devopscicd15](./images/devopscicd15.PNG)

* __MAVEN BUILD LIFECYCLE__
1. Default
  1. validate
  2. intialize
  3. generate-sources
  4. process-sources
  5. generate-resources
  6. process-resources
  7. compile
  8. process-clasess
  9. generate-test-sources
 10. test
 11. package
 12. verify
 13. install
 14. deploy
2. Clean 
  1. pre-clean
  2. clean
  3. post-clean
3. Site ( we dont use it is for documentation purpose )
  1. pre-site 
  2. site
  3. post-site
  4. site-deploy

![devopscicd16](./images/devopscicd16.PNG)

* __POM.XML__  Project Object Model it is an xml file it contains information about the project  and configuration details used by maven to build the project , it contains default values for most projects.
* it teling about inforamation what project does do what is artifact id and version and also configuration which u need to execute the project and it also contain default value which are requierd to that project 

* __Transitive Dependency__ when ever u callin some dependencies in pom.xml it will bring some more dependencies that is called transitive dependency.

* __LOCAL REPOSITORY__ VS __REMOTE REPOSITORY__
* when ever we run maven project first time it is going to create a local repository by default local repository get created __users/basha/.m2/repository__ when ever we requier any dependencies mention in pom.xml it pull from remote repository to local repository 
* if u want to keeps file into our .m2 directory then we can use __install__ 

![devopscicd17](./images/devopscicd17.PNG)

JAVE SETUP
* sudo apt install java-1.8*
* java -version
* find /usr/lib/jvm/java-1.8* | head -n 3 
* vi ~/.bash_profile
* JAVA_HOME=/USR/LI/JVM/JAVA-1.8.0-OPENJDK-1.8.0.272.b10-1.amzn2.o.1.x86_64
* PATH-$PATH:$HOME/bin:$JAVA_HOME
* source ~/.bash_profile
* echo $PATH

MAVEN SETUP
* wget tar
* tar -xvzf filename.gz
* /opt/apache-maven-3.6.3
* vi ~/.bash_profie
* M2_HOME=/opt/apache-maven-3.6.3
* M2=/opt/apache-maven-3.6.3/bin
* PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2
* source ~/.bash_profile 
* echo $PATH 
* mvn --version

* __settings.xml__ pom.xml assoiciated with specific project if u use that pom.xml other project  may or may not work 
* but __Settings.xml__ is global configuration assume that there are some common values need to provide accrocss ur environment then u can update in __Settings.xml__ file 
* this file configure in 2 locataion 
  * the maven install: __${maven.home}/conf/settings.xml__
    * cd /opt/apache-maven-3.6.3/
    * cd conf 
    * settings.xml
  * A user's install: __${user.home}/.m2/settings.xml__  
    * cd .m2
    * here also u can create by default u cant see settings.xml file but we can create 

Tomcat-installation: https://github.com/ravdy/maven/blob/master/tomcat_installation.MD

Jenkins-installation: https://github.com/ravdy/maven/blob/master/jenkins_installation.MD


* jenkins slav node   
* useradd jenkins
* passwd jenkins
* visudo 
* root ALL=(ALL)   ALL
* jenkins   ALL=(ALL)   NOPASSWD: ALL
* vi /etc/ssh/sshd_config
* PasswordAuthentication yes
* // # PasswordAuthentication no
* service sshd reload 

#### ARTIFACTORY
* when ever developer develop the code its available in sourcecode it is available in readable format
* it is a source code where they develop code and they can use that one build a artifact to build a artifact we need to some activity in between nothing but compilation when ever we compile any source code if source code is fine it is generate the outcome the outcome whcih comes outof source code we callit as artifact 
* we have java code when u build java code u get a .jar or .war or .ear 
* .net we get .exe 
* why do we need artifat why cant we use source code becouse sourcecode is not understandble by ur system, 
* ur system cant understand source code that why we need to convert our source code into system understandble  lanuage 
* if we share source code directly there is possible for every one can use source code and create same application with other name so we loss business 
* when we do compilation the compiler can able to understand source code and it converts into binery(nothing but zero ones) those binery can understand by ur system 
* all the artifact doesnt convert into binerys becouse some binerys or some artifacs understandbe by application 
* when ever u want to install java application u need a some application server  why application server even though jar or war files those are not understandble by ur system directly the application server will understand thats reson when ever we install java application we all going to use application server like tomcat, websepar, web logic all this applicaton server 

* what is artifactory repository?
* we can store outcome of artifacts as well as to build we need some dependencies that dependeices we can store in artifactory like maven remote repository 
* sotre libreis required fo rbuild 

* ./artifatory.sh start
* netstat -tulpn u can see wich ports are using 
* username admin
* password password
* when create repositories in jforg-artifactory with maven it will create   
  1. libs-snapshot-local
  2. libs-release-local
  3. jcenter
  4. libs-snapshot 
  5. libs-release
* artifactory
  1. local    ( )
     * libs-release-local
     * libs-snapshot-local
  2. remote   ( )
     * jcenter
  3. virtual  (combination of loacl and remote)
     * libs-release
     * libs-snapshot
* to intigrate with maven we need update in pom.xml file 
* maven communicate with __libs-release-local__ __libs-snapshot-local__ u need to generate the pom.xml like code or in jfrog artifactory u have feature to generate the code for that __SetMeUp__ -> select tool maven -> generate maven settings -> select repository -> then u will get distrubution management -> copy -> update in pom.xml after dependecy -> 
* what we are saying maven u can build it what ever outcome ur getting that out come u need to store on jfrog artifactory  (<url>http://ec2-12-233-23-103.ap.south-1compute.amazonaws.com:8081/artifactory/libs-snapshot-local</url>)
* we mention jfrog artifactory server details but maven should have access like when we login it will ask username and password for that create new user  -> admin -> new -> maven -> admin privileges -> password -> email -> save ->  use this user to communicate maven to jfrog artifactory 
* to provide the credentials to maven there is file called __settings.xml__ that fie u need to store in __.M2__ folder so that can able to authenticate with artifactory 
* to get __settings.xml__  repositorys -> libs-snapshot-local -> SetMeUp -> generate maven settings ->   generate settings -> it will give snippet copy   ->.me/ vi settings.xml past replace username and password
```
<username>maven</username>
<password>Maven@123</password>
```
* what we are saying to maven use this __libs-snapshot-local__ repository to store snapshots  
* __SetMeUp__ option is very usefull when ever we generate the code which is requeired to communicate with pur tools 
* mvn deploy it create repository and it deploys in the target location 
*  why we storeing artifact into artifatory  we need to maintain version 1.10