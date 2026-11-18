
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded successfully'
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

        stage('Docker Check') {
            steps {
                bat '"C:\\Users\\User\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" version'
            }
        }

        stage('Docker Build') {
            steps {
                bat '"C:\\Users\\User\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t hospital-management-system:jenkins .'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                "C:\\Users\\User\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" rm -f hospital-jenkins-app 2>NUL
                "C:\\Users\\User\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" run -d --name hospital-jenkins-app -p 8089:8087 -v hospital-db-data:/app/data hospital-management-system:jenkins
                '''
            }
        }
    }

    post {
        success {
            echo 'Hospital Management System deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
