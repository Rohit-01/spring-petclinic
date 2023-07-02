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
        sh '''mvnw verify sonar: sonar \\
  -Dsonar.projectKey=Petcliinic \\
  -Dsonar.projectName=\'Petcliinic\' \\
  -Dsonar.host.url=http://172.31.16.5:9000 \\
  -Dsonar.token=sqp_e528eb2187ffc09372eb1755bb21a8bd9054c9ba'''
      }
    }

  }
}