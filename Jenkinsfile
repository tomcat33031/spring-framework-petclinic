pipeline {
  agent any
  tools { 
    maven 'M3' 
  }  
  stages {
    stage ('Build & Unit test'){
      steps {
        sh 'mvn clean verify -DskipITs=true';
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.war'
      }
    }  
  }
}
