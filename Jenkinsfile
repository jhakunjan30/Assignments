node{
  stage('SCM Checkout'){
    git 'https://github.com/jhakunjan30/assignments/new/master/FirstWebApp'
  }
  stage('Compile-Package'){
    def mvnHome = tool name: 'Maven3', type: 'maven'
    sh "${mvnHome}/bin/mvn package"
  
  }
}
