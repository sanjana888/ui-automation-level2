pipeline {
    agent any

    stages {

        stage('Install Python & Dependencies') {
            steps {
                sh '''
                python3 --version
                pip3 --version
                pip3 install --upgrade pip
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Pytest Tests') {
            steps {
                sh '''
                python3 -m pytest -n 2 --alluredir=reports/allure-results
                '''
            }
        }

        stage('Generate Allure Report') {
            steps {
                allure includeProperties: false,
                       jdk: '',
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