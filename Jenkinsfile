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
    stage("Test") {
       steps {      
	 Parallel (
		"step 1": { echo 'Testing the Applications Test-1' },
	  	"step 2": { echo 'Testing the Applications Test-2' },
                "step 3": { echo 'Testing the Applications Test-3' },
                "step 4": { echo 'Testing the Applications Test-4' }
                )
            }
	  }
	 
      stage("Deploy") {
      steps {
	    Parallel (
		"step 1": { sh "cp zorg.txt zorg1.txt" },
	  	"step 2": { sh "cp zorg.txt zorg2.txt" },
                "step 3": { sh "cp zorg.txt zorg3.txt" },
                "step 4": { sh "cp zorg.txt zorg4.txt"}
                )
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
