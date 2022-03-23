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
   stage ('Code coverage')  {
       jacoco()
   }

   stage ('Nexus upload')  {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '52.91.206.0:8081',
        groupId: 'com.example.maven-project',
        version: '1.0-SNAPSHOT',
        repository: 'http://52.91.206.0:8081/repository/maven-snapshots/',
        credentialsId: 'nexus',
        artifacts: [
            [artifactId: 'webapp',
             classifier: '',
             file: '/var/lib/jenkins/workspace/demo/webapp/target/webapp.war',
             type: 'war']
        ]
     )
    }
    stage ('DEV Deploy')  {
      echo "deploying to DEV Env "
      deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://34.239.132.43:8090/')], contextPath: null, war: '**/*.war'
    }
}
