pipeline {
  
  agent any
  
  stages {
    
    stage("build") {
      steps {
        echo 'Building the application...'
      }
    }
    stage("test") {
      steps {
        echo 'Testing the Applications....'
      }
    }
    stage("deploy") {
      steps {
        echo 'Deploying the application...'
      }
    }
    stage('cat README') {
      when {
        branch "release"
      }
      steps {
        sh '''
        cat Readme.md
        '''
      }
    }
  }
}
