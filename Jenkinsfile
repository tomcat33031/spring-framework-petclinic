pipeline {
  agent any
  tools { 
    maven 'M3' 
  }  
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Result') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.war'
      }
    }

  }
}
