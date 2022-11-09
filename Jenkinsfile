pipeline{
    agent any
    stages{
        stage("sonar_quality_check"){
            agent {
                docker{
                    image'openjdk:11'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                            sh 'chmod +x gradlew'
                            sh './gradlew sonarqube'
                    }

                }
            }
        }
    }
}