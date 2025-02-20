pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat './mvnw clean install'
            }
        }
        stage('Code Coverage') {
            steps {
                bat './mvnw test'
            }
            post {
                always {
                    publishCoverage adapters: [jacocoAdapter('**/target/site/jacoco/jacoco.xml')]
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
