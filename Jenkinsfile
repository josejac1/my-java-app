pipeline {
    agent any
    tools {
        maven 'Maven' // Assumes Maven is configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/YOUR_USERNAME/my-java-app.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Assumes SonarQube is configured
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    docker.build("YOUR_DOCKERHUB_USERNAME/my-java-app:latest")
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-cred') {
                        docker.image("YOUR_DOCKERHUB_USERNAME/my-java-app:latest").push()
                    }
                }
            }
        }
    }
}