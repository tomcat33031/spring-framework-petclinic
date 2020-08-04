pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        tool 'M3'
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