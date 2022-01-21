pipeline{
    agent any
    stages{
        stage ('Checkout Code'){
            steps{
                git branch: 'devops', 
                    url: 'https://github.com/kelvinduan2020/CICD_Java_gradle_application.git'
            }
        }
        
        stage("Sonar Quality Check"){
            steps{
                script{
                    withSonarQubeEnv('sonarqube-server') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                }
            }
        }
    }
}
