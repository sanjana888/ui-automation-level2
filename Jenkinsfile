pipeline {
    agent {
        docker {
            image 'python:3.10'
            args '-u root'
        }
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh '''
                python --version
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Pytest Tests') {
            steps {
                sh '''
                pytest -n 2 --alluredir=reports/allure-results
                '''
            }
        }

        stage('Generate Allure Report') {
            steps {
                allure includeProperties: false,
                       results: [[path: 'reports/allure-results']]
            }
        }

    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Tests executed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}