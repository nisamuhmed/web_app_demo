pipeline {
    agent any

    
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/nisamuhmed/web_app_demo.git'
            }
        }
        
        stage('Build Image') {
            steps {
                sh 'docker build . -t zomato_web_demo' 
            }
        }

        stage('Run Container ') {
            steps {
                sh 'docker rm -f zomato_web_app'
                sh 'docker run -d --name zomato_web_app -p 3000:3000 zomato_web_demo' 
            }
        }
                
        stage('Install dependencies') {
            steps {
                sh 'npm install' 
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm run build' 
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'cp -r build/* /var/www/html' 
            }
        }
        
    }
}
