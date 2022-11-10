pipeline{
    agent any
    stages{
        stage("sonar_quality_check"){
            agent {
                docker {
                    image'openjdk:11'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'token1') {
                            sh 'chmod +x gradlew'
                            sh './gradlew clean build -d sonarqube'
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