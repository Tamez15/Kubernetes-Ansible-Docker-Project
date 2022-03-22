node {
    def mvnHome = tool 'Maven'
    stage ("checkout")  {
      checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/Tamez15/Cucumber.git']]])
    }
     stage ('build')  {
      sh "${mvnHome}/bin/mvn clean install "
    }
}

