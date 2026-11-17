
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd -B clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                bat 'mvnw.cmd -B test'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t hospital-management-system:jenkins .'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker rm -f hospital-jenkins-app 2>NUL
                docker run -d --name hospital-jenkins-app -p 8089:8087 -v hospital-db-data:/app/data hospital-management-system:jenkins
                '''
            }
        }
    }

    post {
        success {
            echo 'Build, Test and Deployment Successful!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}
