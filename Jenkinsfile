pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sanjana888/ui-automation-level2.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 --version
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                pytest -n 2 --alluredir=allure-results
                '''
            }
        }

        stage('Generate Allure Report') {
            steps {
                sh '''
                allure generate allure-results --clean -o allure-report
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'allure-report/**', fingerprint: true
        }
    }
}