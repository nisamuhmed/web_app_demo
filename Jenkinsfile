pipeline {
    agent any
    
    environment {
        PREVIOUS_COMMIT = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Git Clone') {
            steps {
                script{
                git branch: 'main', url: 'https://github.com/nisamuhmed/web_app_demo.git'
                }
            }
        }
        
        stage('Build Image') {
            steps {
                script{
                    CURRENT_COMMIT = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    if (CURRENT_COMMIT != PREVIOUS_COMMIT) {
                        // Only execute build steps if changes are detected
                    sh 'docker build -t zomato_web_demo .'
                    } else {
                        echo 'Skipping build stage as no changes detected.'
                    }
                }
            }
        }
        
        stage('Run Container') {
            steps {
                script {
                    CURRENT_COMMIT = sh(script: 'git rev-parse HEAD', returnStdout: true).trim()
                    if (CURRENT_COMMIT != PREVIOUS_COMMIT) {
                        // Only deploy if changes are detected
                        sh 'docker rm -f zomato_web_app'
                        sh 'docker run -d --name zomato_web_app -p 3000:3000 zomato_web_demo'
                    } else {
                        echo 'Skipping deploy stage as no changes detected.'
                    }
                }
            }
        }
    }
}
