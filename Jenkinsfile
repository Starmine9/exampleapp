pipeline {
    agent any

    environment {
        APP_NAME = "exampleapp"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t $APP_NAME:latest -f Dockerfile $APP_NAME"
            }
        }

        stage('Run Containers') {
            steps {
                sh """
                # Stop old containers if running
                docker stop $APP_NAME || true

                # Run new containers
                docker run -d --rm --name $APP_NAME -p 3000:3000 $APP_NAME:latest
                """
            }
        }
    }
}
