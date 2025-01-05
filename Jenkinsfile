pipeline {
    agent any

    stages {
        stage('Start Grid'){
            steps {
                bat "docker compose -f grid.yaml up -d"
            }
        }

        stage('Run Tests'){
            steps {
                bat "docker compose -f test-suites.yaml up"
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
            bat "docker compose -f grid.yaml down"
            bat "docker compose -f test-suites down"
        }
    }
}