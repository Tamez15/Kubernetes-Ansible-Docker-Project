pipeline {
  agent any
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
