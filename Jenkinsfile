pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = "1ms24mc020"
        IMAGE_NAME = "my_web_app"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Charitha1705/my_web_app.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKERHUB_USERNAME}/${IMAGE_NAME}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline Successful 🎉"
        }
        failure {
            echo "Pipeline Failed ❌"
        }
        always {
            echo "Cleaning Up Workspace"
            deleteDir()
        }
    }
}
