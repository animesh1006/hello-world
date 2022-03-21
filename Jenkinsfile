pipeline {
  
  agent any
  
  stages {
    
    stage("build") {
      node {
     // Checkout
      checkout scm
     // install required bundles
     sh ‘bundle install’
     // build and run tests with coverage
     sh ‘bundle exec rake build spec’
    // Archive the built artifacts
     archive (includes: ‘pkg/*.gem’)
     // Archive the built artifacts
     archive (includes: ‘pkg/*.gem’)
    // publish html
     publishHTML ([
     allowMissing: false,
     alwaysLinkToLastBuild: false,
     keepAll: true,
     reportDir: ‘coverage’,
     reportFiles: ‘index.html’,
     reportName: “RCov Report”
       ])
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
  stage('Download') {
            steps {
                sh 'echo "artifact file" > generatedFile.txt'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'generatedFile.txt', onlyIfSuccessful: true
        }
    }
}
