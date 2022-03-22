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
    
	  stage('write') {
           steps {
               script {
                   def date = new Date()
                   def data = "Hello World\nSecond line\n" + date
                   writeFile(file: 'zorg.txt', text: data)
                   sh "ls -l"
               }
           }
	  }
       stage('read') {
           steps {
               script {
                   def data = readFile(file: 'zorg.txt')
                   println(data)
               }
           }
       }
   	  
    stage("build") {
	steps {
        echo 'Building the application...'
        slackSend channel: "#cicd", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
      	}
      }
    stage("test") {
      steps {
        echo 'Testing the Applications....'
      }
    }
	parallel (
		"Test-1" : {
	  echo 'Testing the Applications Test-1'
    	    },
	    "Test-2" : {
	  echo 'Testing the Applications Test-2'
    	    },
	    "Test-3" : {
	  echo 'Testing the Applications Test-3'
    	    },
	   "Test-4" : {	
	   echo 'Testing the Applications Test-4'
	   }
	)
      }
      stage("deploy") {
      steps {
        echo 'Deploying the application...'
           }
    	}
 stage("Parallel") {
steps {
parallel (
"firstTask" : {
sh "cp zorg.txt zorg1.txt"
},
"secondTask" : {
sh "cp zorg.txt zorg2.txt"
},
"thirdTask" : {
sh "cp zorg.txt zorg3.txt"
},
"fourthTask" : {
sh "cp zorg.txt zorg4.txt"
}
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


