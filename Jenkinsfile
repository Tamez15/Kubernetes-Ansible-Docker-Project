node {
    
    def mvnHome = tool 'Maven'
    stage ("checkout")  {
       checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/Tamez15/Kubernetes-Ansible-Docker-Project.git']]])
    }
     stage ('build')  {
    sh "${mvnHome}/bin/mvn clean install -f webapp/pom.xml"
    }
    stage ('Code Quality scan') {
       withSonarQubeEnv('sonarqube') {
       sh "${mvnHome}/bin/mvn -f webapp/pom.xml sonar:sonar"
        }
   }
}
