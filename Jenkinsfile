pipeline {
  
  agent any
  environment {
    NEW_VERSION = '1.1.0'
	    }
  parameters {
    booleanParam(name:'executeTests',defaultValue:true, description:'Test execution')
  	}
  stages {
    
    stage("build") {
	steps {
        echo 'Building the application...'
        echo 'Building Version ${NEW_VERSION}'
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
	
	  post {
            success {
                slackSend "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        }
	  post {
            failure {
                slackSend failOnError:true message:"Build failed  - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        }
    }
  }
