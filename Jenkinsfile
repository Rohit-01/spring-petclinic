pipeline {
  agent {
    node {
      label 'test-node'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=Petcliinic \\
  -Dsonar.projectName=\'Petcliinic\' \\
  -Dsonar.host.url=http://172.31.16.5:9000 \\
  -Dsonar.token=sqp_e528eb2187ffc09372eb1755bb21a8bd9054c9ba'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/*.xml'
            perfReport '**/target/jmeter/results/*'
          }
        }

      }
    }

  }
}