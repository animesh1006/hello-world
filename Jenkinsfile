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
        // test variable: 0=success, 1=fail; must be string
        doError = '0'
        BUILD_USER = ''
    	}

  agent any
  
  parameters {
    booleanParam(name:'executeTests',defaultValue:true, description:'Test execution')
  	}
  stages {
	  
	  stage("Build1") {
           steps {
		   echo 'Building the application Write...'
               script {
                   def date = new Date()
                   def data = "Hello World\nSecond line\n" + date
                   writeFile(file: 'zorg.txt', text: data)
                   sh "ls -l"
                   }
	       }
	  }
       stage("Build2") {
           steps {
		   echo 'Building the application Read...'
               script {
                   def data = readFile(file: 'zorg.txt')
                   println(data)
               }
           }
       }
       stage("Message") {
	steps {
        echo 'Sending message over Slack...'
        slackSend channel: "#cicd", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
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
        }

stage("Build") {
            parallel {
                stage('Build 1') {
                    steps { sh 'echo Build-1' }
                }
                stage('Build 2') {
                    steps { sh 'echo Build-1' }
                }
                stage('Build 3') {
                    steps { sh 'echo Build-1' }
                }
                stage('Build 4') {
                    steps { sh 'echo Build-1' }
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
		
   // Post-build actions
post {
        always {
             echo 'Pipe line completed'
        }
    }
}
