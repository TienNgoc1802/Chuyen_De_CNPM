pipeline {
    agent any

    environment {
        CONTAINER_NAME="my-app"
        DATABASE_NAME="MyDatabase"
        DATABASE_PASSWORD="abc123456"
        DATABASE_ROOT_PASSWORD="root_password"
        DATABASE_USER="admin"
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'dfefc008-1ed5-4114-8fd9-0caca08c7f12', url: 'https://github.com/TienNgoc1802/Chuyen_De_CNPM.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    bat 'docker-compose down'
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/logs/**', allowEmptyArchive: true
        }
    }
}
