pipeline {
  agent any
    tools {
      maven 'mymaven'
    }
    stages {
          stage('preparation of code checkout'){
               steps {
            
                   git 'https://github.com/prashanth-1993/hello-world-servlet.git'
                }
           }
      
     stage ('building the code') {
       steps {
         sh 'mvn install'
         
       }
     }
      stage ('unit tests'){
        steps {
         junit '**/target/surefire-reports/TEST-*.xml'
        }
      }
      stage ('Artifact uploader'){
      
        steps {
          nexusPublisher nexusInstanceId: '12315', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '\'**//target/*.war\'']], mavenCoordinate: [artifactId: 'hello-world-servlet-example', groupId: 'com.geekcap.vmturbo', packaging: 'war', version: '$BUILD_ID']]]
        }
      }
    
    
    } 
  
 }
