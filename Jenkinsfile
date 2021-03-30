pipeline {
    agent any 
    tools{
        jdk "JAVA 1.8"
    }
    stages {
        stage('Clean') { 
            steps {
                //
              bat "mvn clean"
            }
        }
        stage('Test') { 
            steps {
                //
              bat "mvn test"
            }
        }
       
        stage('Package') { 
            steps {
                //
              bat "mvn package -f FirstWebApp"
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv(credentialsId:'sonar2',installationName: 'sonar_server')
               
                {
                    bat "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.10.0:sonar "
                     

 

               }}}
        
        
        stage('upload to artifactory'){
               
           steps{
      rtUpload (
                    serverId: 'artifactory_server',
                    spec: '''{
                        "files": [
                            {
                            "pattern": "./target/*.war",
                            "target": "example-repo-local"
                            }
                        ]
                    }''',
                    failNoOp: true,
                )
                rtPublishBuildInfo (
                    serverId: 'artifactory_server',
                )
           }
           }
    }
}
