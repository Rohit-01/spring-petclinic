pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petcliinic \\
  -Dsonar.projectName=\'Petcliinic\' \\
  -Dsonar.host.url=http://172.31.16.5:9000 \\
  -Dsonar.token=sqp_f7dce25fa7beb238ee716ba3ccb666939266e9f9'''
      }
    }

  }
}