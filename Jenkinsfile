pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean install'
            }
        }
        stage('Code Coverage') {
            steps {
                jacoco()
            }
            post {
                always {
                    jacoco execPattern: '**/target/*.exec'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
    }

    triggers {
        cron('H/10 * * * 1')
    }
}
