pipeline {
agent any
stages {
 stage("Code Checkout from GitLab") {
  steps {
   git branch: 'master',
    url: 'https://github.com/haseebsultan/the-example-app.nodejs.git'
  }
 }
   stage('Code Quality Check via SonarQube') {
   steps {
       script {
       def scannerHome = tool 'SonarQube';
           withSonarQubeEnv("SonarQube") {
           sh "${tool("SonarQube")}/bin/sonar-scanner \
           -Dsonar.projectKey=nodeJS \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://52.203.65.180:9000 \
           -Dsonar.login=abb8bd0edcabbc6c389c83db64cc2819268e9a0f"
           
               }
           }
       }
   }
 
}
}
