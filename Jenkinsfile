pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                // Your build commands go here
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                // Your testing commands go here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
                // Your deployment commands go here
            }
        }
    }
    post {
        always {
            // Send an email regardless of the build result
            mail to: 'commanderata@gmail.com',
                 subject: "Build ${currentBuild.fullDisplayName}",
                 body: "The build was ${currentBuild.result}: Check Jenkins for details."
        }
        success {
            // Additional actions for successful build
            echo 'ohohoho'
            // Load and execute Jenkinsfile1
            script {
                load 'Jenkinsfile1'
            }
        }
        failure {
            // Additional actions for failed build
            echo 'hahaha..'
        }
    }
}
