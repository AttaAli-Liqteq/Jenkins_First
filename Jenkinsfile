pipeline {
    agent any 

    environment {
        // Define environment variables if needed
        PROJECT_DIR = '/home/attaali/Desktop/Node_Basic'
    }

    stages {
        stage('Prepare Environment') {
            steps {
                // Create the project directory if it doesn't exist
                sh 'mkdir -p $PROJECT_DIR'
            }
        }

        stage('Clone Repository') {
            steps {
                // Change to the project directory and clone the repo
                // Replace 'yourusername/yourrepository.git' with your actual repository path
                script {
                    dir('$PROJECT_DIR') {
                        sh 'git clone https://github.com/yourusername/yourrepository.git . || git pull'
                    }
                }
            }
        }

        stage('Build and Run Docker Containers') {
            steps {
                // Navigate to the project directory and run docker-compose
                sh 'cd $PROJECT_DIR && docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up'
            // Add any cleanup steps if required
        }
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
