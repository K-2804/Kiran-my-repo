pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the GitHub repository...'
                git branch: 'main', url: 'https://github.com/K-2804/Kiran-my-repo.git'
            }
        }

        stage('Build and Run Containers') {
            steps {
                script {
                    echo 'Building and starting Docker containers...'
                    sh 'docker-compose down || true' // Stops running containers if any
                    sh 'docker-compose up -d --build' // Builds and runs containers
                }
            }
        }

        stage('Test API') {
            steps {
                script {
                    echo 'Testing the Flask API...'
                    sh 'curl -f http://localhost:5000/users' // Tests the `/users` endpoint
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline Completed!'
        }
        success {
            echo 'Pipeline ran successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
