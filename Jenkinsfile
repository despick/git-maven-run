pipeline {
  agent {
    docker {
      image 'java'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn package'
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Firefox": {
            sh 'mvn test'
            
          },
          "Chrome": {
            sh 'mvn test chrome'
            
          },
          "IE": {
            sh 'mvn test ie'
            
          }
        )
      }
    }
    stage('Publish') {
      steps {
        junit(allowEmptyResults: true, testResults: '**/test-results.xml')
      }
    }
  }
}