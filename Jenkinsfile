pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "rakhamajigavade45@gmail.com"
        PORT = "3000"
    }

    stages {
        stage ('Clone Repo') {
            steps {
                git branch: 'main' , url:'https://github.com/11Abhi55/CI-CD-using-all-'
            }
        }

        stage ('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME'
            }
        }

        stage ('Stop and Remove Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage ('Docker Container Run') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT}
                    --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

         stage ('Send Email Notification') {
            steps {
                emailtext (
                    subject: "Nestjs App deployed Succusefully
                    on Ec2 Instance"
                    body: "Your Nestjs app deployed succussfully 
                    on port http://13.63.161.88:${PORT}"
                    to: ${Email}
                )
            }
        }
    }
}