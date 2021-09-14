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
              // requires SonarQube Scanner 2.8+
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
        stage('Install Docker and Docker-compose'){
            steps{
                sh 'ansible-playbook -i hosts azure-docker.yml'
                sh 'sleep 45'
            }
        }
        
        stage('Build images by dockerfiles'){
            steps{
                sh 'ansible-playbook -i hosts buildImages.yml'
            }
        }
        
        stage('Run Docker Compose'){
            steps{
                sh 'ansible-playbook -i hosts runContainers.yml'
            }
        }
    }
}
