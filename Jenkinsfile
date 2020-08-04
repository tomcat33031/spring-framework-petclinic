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
    stage('Static Code Analysis'){
      steps {
        sh 'mvn clean verify sonar:sonar -Dsonar.projectName=petclinic-project -Dsonar.projectKey=petclinic-project -Dsonar.projectVersion=$BUILD_NUMBER';
      }
    }
  }
}
