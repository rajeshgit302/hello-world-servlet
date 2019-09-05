pipeline {
    agent any 
    tools { 
        maven 'maven' 
      
    }
stages { 
     
 stage('Preparation') { 
     steps {
// for display purposes

      // Get some code from a GitHub repository

      git 'https://github.com/prashanth-1993/hello-world-servlet.git'

      // Get the Maven tool.
     
 // ** NOTE: This 'M3' Maven tool must be configured
 
     // **       in the global configuration.   
     }
   }

   stage('Build') {
       steps {
       // Run the maven build

      //if (isUnix()) {
         sh 'mvn -Dmaven.test.failure.ignore=true install'
      //} 
      //else {
      //   bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
       }
//}
   }
 
  stage('Results') {
      steps {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.war'
      }
   } 
    
stage('sonarqube') {
        environment {
          scannerHome = tool 'sonar'
         }
    steps {
         withSonarqubeEnv('sonar') {
            sh "${scannerHome}/bin/sonar-scanner"
         }
         timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
          }
     }
}
    
   stage('Artifact upload') {
        steps {
     nexusArtifactUploader artifacts: [[artifactId: 'hello-world-servlet-example', classifier: '', file: '*/target/helloworld.war', type: 'war']], credentialsId: '47a08872-a5a7-4b59-8691-4da41fb05bd3', groupId: 'com.geekcap.vmturbo', nexusUrl: '18.185.130.154:8081/nexus/content/repositories/releases/', nexusVersion: 'nexus2', protocol: 'http', repository: 'releases', version: '1.0-SNAPSHOT'
      }
 }
}
}

