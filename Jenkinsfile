pipeline {
    agent any

    stages {

     stage('Clone Repo') {
    steps {
        git branch: 'main',
            url: 'https://github.com/sanjana888/ui-automation-level2.git'
    }
}

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest --alluredir=reports/allure-results'
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
}