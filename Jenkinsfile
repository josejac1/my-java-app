pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/josejac1/my-java-app.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    docker.build("YOUR_DOCKERHUB_USERNAME/my-java-app:${env.BUILD_NUMBER}")
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-cred') {
                        docker.image("YOUR_DOCKERHUB_USERNAME/my-java-app:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
