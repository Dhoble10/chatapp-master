pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dhoble10/chatapp-master.git', credentialsId: '20e9b267-e8f7-410b-84ee-c59dd65ba49c'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('src') {
                    bat 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('src') {
                    bat 'npm run build'
                }
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('server') {
                    bat 'npm install'
                }
            }
        }

       stage('Start Backend Server') {
  steps {
    bat 'start /B npm run server'  // /B runs in the same window without a new console
  }
}


        stage('Start Frontend Server') {
            steps {
                dir('src') {
                    bat 'npm run dev &'
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
