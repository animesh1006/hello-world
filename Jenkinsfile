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
        echo 'Building Version ${NEW_VERSION}'
		slackSend channel: "#cicd", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
      	}
      }
    
    stage("test") {
      when {
        expression {
          params.executeTests
	      }
	   }
      steps {
	 
        echo 'Testing the Applications Test-1'
    	    }
	 }
    	  post {
	always {
	    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
	}
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
        // Let's wipe out the workspace before we finish!    deleteDir()
                echo "Workspace cleaned"
       	   }
     }
}

