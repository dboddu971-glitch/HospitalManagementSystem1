
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
