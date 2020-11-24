pipeline {
agent any
tools {nodejs "NodeJS"} 
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
        qualitygate = waitForQualityGate()
            if (qualitygate.status != "OK") {
              currentBuild.result = "FAILURE"
              slackSend (channel: '****', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://****.com:9000/sonarqube/projects|Review in SonarQube>.")
            }
           }
       }
   }
 stage("Install Project Dependencies") {
   steps {
       nodejs(nodeJSInstallationName: 'NodeJS'){
           sh "npm install"
           }
       }
   }
}
}
