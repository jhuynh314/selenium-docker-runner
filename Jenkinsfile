pipeline {
    agent any

    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
    }

    stages {
        stage('Start Grid'){
            steps {
                bat "docker compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
            }
        }

        stage('Run Tests'){
            steps {
                bat "docker compose -f test-suites.yaml up --pull=always"
                script {
                    if(fileExists('output/flight-reservation/testng-failed.xml') || fileExists('output/vendor-portal/testng-failed.xml')){
                        error('failed tests founds')
                    }
                }
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
            bat "docker compose -f test-suites.yaml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}