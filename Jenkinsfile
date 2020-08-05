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
        withSonarQubeEnv('sonarqube') {
          sh 'mvn clean verify sonar:sonar -Dsonar.projectName=petclinic-project -Dsonar.projectKey=petclinic-project -Dsonar.projectVersion=$BUILD_NUMBER';
        }
      }
    }
    stage ('Integration Test'){
      steps {
        sh 'mvn clean verify -Dsurefire.skip=true';
        //junit '**/target/failsafe-reports/TEST-*.xml'
        archiveArtifacts 'target/*.war'        
      }
    }
    stage ('Publish'){
      steps {
        rtUpload(
          serverId: 'Artifactory Server',
          spec: """{
            "files": [
              {
                "pattern": "target/petclinic.war",
                "target": "petclinic-project/${BUILD_NUMBER}/",
                "props": "Integration-Tested=Yes;Performance-Tested=No"
              }
            ]
          }"""
        )
      }
    }    
  }
}
