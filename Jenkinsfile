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
                script {thi
                    dir("${WORKSPACE}/Node_Basic") {
                        // Using the checkout step for a more Jenkins-native approach
                        checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],
                            userRemoteConfigs: [[url: 'https://github.com/AttaAli-Liqteq/Jenkins_First.git']]]
                    }
                }
            }
        }

        stage('Build and Run Docker Containers') {
            steps {
                script {
                    // Build the Node.js application Docker image
                    sh "docker build -t node_app_image -f ${PROJECT_DIR}/Dockerfile ${PROJECT_DIR}"
                    // Run the Node.js application Docker container
                    sh "docker run -d --name node_app_container -p 3000:3000 node_app_image"
                    
                    // Build the PostgreSQL Docker image
                    sh "docker build -t postgres_image -f ${PROJECT_DIR}/Dockerfile1 ${PROJECT_DIR}"
                    // Run the PostgreSQL Docker container
                    sh "docker run -d --name postgres_container -p 5432:5432 postgres_image"
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up'
            // Add cleanup steps for Docker containers if required
            sh 'docker stop node_app_container || true && docker rm node_app_container || true'
            sh 'docker stop postgres_container || true && docker rm postgres_container || true'
        }
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
