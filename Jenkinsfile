pipeline{
  agent any
  stages{
    stage('Checkout SCM'){
      steps{
        git url: 'https://github.com/abhirom/example-voting-app.git'
      }
    }
    stage('SonarQube analysis') {
         steps {
            script {
              scannerHome = tool 'sonarqube'
            }
            withSonarQubeEnv('sonarqube') {
             sh "${scannerHome}/bin/sonar-scanner \
             -D sonar.login=admin \
             -D sonar.password=admin \
             -D sonar.projectKey=sonarqube"
            }
          }
        }
  }
}

