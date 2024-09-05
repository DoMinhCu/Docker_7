pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git 'https://github.com/DoMinhCu/Docker_7.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image from Dockerfile
                    docker.build("your-image-name")
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                script {
                    // Run unit tests (if applicable)
                    sh 'npm test'
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    // Build the React app using Dockerfile
                    sh 'docker run --rm your-image-name npm run build'
                }
            }
        }
        
        stage('Deploy to Nginx') {
            steps {
                script {
                    // Deploy built app to Nginx container
                    sh '''
                    docker run -d --name your-nginx-container -p 80:80 \
                    --rm your-image-name
                    '''
                }
            }
        }
    }
    
    post {
        always {
            // Clean up after pipeline completion
            script {
                sh 'docker stop your-nginx-container || true'
            }
        }
    }
}
