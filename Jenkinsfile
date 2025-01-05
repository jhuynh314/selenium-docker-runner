pipeline {
    agent any

    stages {
        stage('Run Test'){
            steps {
                bat "docker compose up"
            }
        }

        stage('Bring Grid Down'){
            steps {
                bat "docker compose down"
            }
        }
    }

    post {
        success{
            echo "I was successful"
        }
        failure{
            echo "I was a failure"
        }
        aborted{
            echo "I was aborted"
        }
        always{
            echo "doing clean up"
        }
    }
}