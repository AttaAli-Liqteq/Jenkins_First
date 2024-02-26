pipeline {
    agent any 
    
environment {
    // Define the project directory within the Jenkins workspace
    PROJECT_DIR = "${WORKSPACE}/Node_Basic"
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
                script {
                    dir("${WORKSPACE}/Node_Basic") {
                        // Using the checkout step for a more Jenkins-native approach
                        checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],
                            userRemoteConfigs: [[url: 'https://github.com/yourusername/yourrepository.git']]]
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
