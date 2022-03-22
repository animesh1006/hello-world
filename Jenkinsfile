def COLOR_MAP = [
    'SUCCESS': 'Good', 
    'FAILURE': 'Danger',
]
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
    // Set up local variables for your pipeline
    environment {
	   ENV_NAME = "${env.BRANCH_NAME}"
   	 // test variable: 0=success, 1=fail; must be string
        doError = '0'
        BUILD_USER = ''
    	}

  agent any
  
  parameters {
    booleanParam(name:'executeTests',defaultValue:true, description:'Test execution')
  	}
   stages {
	
	   stage('Build Container') {
            steps {
                echo 'Building Container..'

                script {
                    if (ENVIRONMENT_NAME == 'develop') {
                        ENV_NAME = 'Development'
                    } else if (ENVIRONMENT_NAME == 'release') {
                        ENV_NAME = 'Release'
                    } else if (ENVIRONMENT_NAME == 'master') {
                        ENV_NAME = 'Master'
                }
                echo 'Building Branch: ' + env.BRANCH_NAME
                echo 'Build Number: ' + env.BUILD_NUMBER
                echo 'Building Environment: ' + ENV_NAME

                echo "Running your service with environemnt ${ENV_NAME} now"
               }
             }
          }
	   
	stage("Testing in Progress") {
            parallel {
                stage('Stage 1') {
                    steps { sh 'echo Test-1 passed' }
                }
                stage('Stage 2') {
                    steps { sh 'echo Test-2 passed' }
                }
                stage('Stage 3') {
                    steps { sh 'echo Test-3 passed' }
                }
                stage('Stage 4') {
                    steps { sh 'echo Test-4 passed' }
                }
            }
     // * success {
     // publishHTML ([
    // allowMissing: false,
    // alwaysLinkToLastBuild: false,
    // keepAll: true,
    // reportDir: ‘coverage’,
    // reportFiles: ‘index.html’,
    // reportName: “RCov Report”
     //  ]) 
        }
// properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '10', 
  //  artifactNumToKeepStr: '10', daysToKeepStr: '7', numToKeepStr: '10']], gitLabConnection('GitLab'), pipelineTriggers([[$class: 'TimerTrigger', spec: 'H 9 * * 1 *']])])
	   
stage("Build") {
	   parallel {
         stage('Build 1') {
                    steps { 
                 script {
                   def date = new Date()
                   def data = "Current date \nSecond line\n" + date
                   writeFile(file: 'zorg.txt', text: data)
                   sh "ls -l"
                   }
                 }
                }
                stage('Build 2') {
                    steps { 
                script {
                   def data = readFile(file: 'zorg.txt')
                   println(data)
        	       }
		    }
           	    }
      		 stage('Build 3') {
                    steps { sh 'echo Build-3' }
                }
                stage('Build 4') {
                    steps { sh 'echo Build-4' }
                }
            }
        }

stage("Distribution") {
               parallel {
                stage('Distribute 1') {
                    steps { sh "cp zorg.txt zorg1.txt"  }
                }
                stage('Distribute 2') {
                    steps { sh "cp zorg.txt zorg2.txt" }
                }
                stage('Distribute 3') {
                    steps { sh "cp zorg.txt zorg3.txt" }
                }
                stage('Distribute 4') {
                    steps { sh "cp zorg.txt zorg4.txt" }
            }
         }
       }

     stage("Message") {
	steps {
        echo 'Sending message over Slack...'
        slackSend channel: "#cicd", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
      	}
      }
  }
		
   // Post-build actions
post {
        always {
             echo 'Pipe line completed'
        }
    }
}
