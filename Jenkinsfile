pipeline {
    agent any

    tools {
        nodejs 'NodeJS_18' // Replace with your configured Node.js version in Jenkins
    }

    environment {
        // Define any necessary environment variables here
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Dhoble10/chatapp-master.git', credentialsId: 'jenkins-github-cicd'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('src') {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('src') {
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('server') {
                    sh 'npm install'
                }
            }
        }

        stage('Start Backend Server') {
            steps {
                dir('server') {
                    sh 'npm run server &'
                }
            }
        }

        stage('Start Frontend Server') {
            steps {
                dir('src') {
                    sh 'npm run dev &'
                }
            }
        }
    }

    post {
        success {
            echo 'Application has been built and started successfully.'
        }
        failure {
            echo 'Build failed. Please check the logs for details.'
        }
    }
}
