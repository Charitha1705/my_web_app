pipeline {
	agent any
	environment {
		DOCKERHUB_CRED=credentials('dockerhub')
		IMAGE_NAME="1ms24mc020/my_web_app:latest ."
	}
	
	stages {
		stage('checkout') {
			steps {
				git url:'https://github.com/Charitha1705/my_web_app.git', branch:'main' 
			}
		}
		
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage=docker.build("${IMAGE_NAME}:latest")
				}
			}
		}
		
		stage('Push to DockerHub') {
			steps {
				script {
					docker.withRegistry('https://index.docker.io/v1/','dockerhub') {
						dockerImage.push()
					}
				}
			}
		}
	}
	
	post {
		success {
			echo "Pipeline Successful"
		}
		failure {
			echo "Pipeline Failed"
		}
		always {
			echo "Cleaning Up WorkSpace"
			deleteDir()
		}
	}
}
