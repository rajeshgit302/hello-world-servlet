pipeline {
  agent any
    tools {
      maven 'mymaven'
    }
    stages {
      stage('preparation')
        steps {
            
          git 'https://github.com/prashanth-1993/hello-world-servlet.git'
        }
    }
}
