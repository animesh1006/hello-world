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
    	   
      stage("deploy") {
      steps {
        echo 'Deploying the application...'
           }
    	}
 stage("Parallel test") {	  
 parallel(firstTask: {
  echo 'Testing the Applications Test-1'
}, secondTask: {
  echo 'Testing the Applications Test-2’
}, ThirdTask: {
  echo 'Testing the Applications Test-3'
}, FourthTask: {
  echo 'Testing the Applications Test-4'
 }
)
 }
  }
   // Post-build actions
post {
    success {
        echo "Test run completed succesfully."
       	 }
     failure {
         echo "Test run failed."
       	  }
     always {
        // Let's wipe out the workspace before we finish!    deleteDir()
                echo "Workspace cleaned"
       	   }
     }
}
