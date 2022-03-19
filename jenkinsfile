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
	    // when { expression { BRANCH_NAME == 'develop'  } } 
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
    }
  }
