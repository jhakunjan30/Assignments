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
              bat "mvn package -f First-Web-App"
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv(installationName: 'sonar_server')
                {
                    bat "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar "
                     -Dsonar.login="b25e9139576b2dea713d400bac1c1f5a63544a1d"

 

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
