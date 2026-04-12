pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Fetching code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building containerized application...'
                sh 'docker-compose -f docker-compose.jenkins.yml build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Starting containers...'
                sh 'docker-compose -f docker-compose.jenkins.yml up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed! App is running on port 8081.'
        }
        failure {
            echo 'Pipeline failed!'
            sh 'docker-compose -f docker-compose.jenkins.yml down'
        }
    }
}
