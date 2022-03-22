pipeline {
  agent any
  environment {
      PATH = "/opt/maven/apache-maven-3.8.5/bin:$PATH"
      }
  stages {
    stage('Maven Version') {
      parallel {
        stage('Maven Version') {
          steps {
            sh 'mvn -v'
          }
        }

        stage('Java Version') {
          steps {
            sh 'java -version'
          }
        }

      }
    }

    stage('Running Test') {
      steps {
        sh 'mvn clean test'
      }
    }
  }
}
