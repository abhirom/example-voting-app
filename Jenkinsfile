pipeline{
  agent any
  stages{
    stage('Checkout SCM'){
      strps{
        git url: 'https://github.com/abhirom/example-voting-app.git'
      }
    }
    stage('SonarQube analysis') {
         steps {
            script {
              // requires SonarQube Scanner 2.8+
              scannerHome = tool 'sonarqube'
            }
            withSonarQubeEnv('sonarqube') {
             sh "${scannerHome}/bin/sonar-scanner \
             -D sonar.login=admin \
             -D sonar.password=password123 \
             -D sonar.projectKey=sonarqube"
            }
          }
        }
  }
}
