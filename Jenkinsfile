pipeline {
    agent any

    environment {
        IMAGE_NAME = 'static-web-app'
        CONTAINER_NAME = 'static-web-test'
        HOST_PORT = '8081'
        CONTAINER_PORT = '80'
    }

    stages {
        stage("Workspace Check") {
            steps {
                echo 'Checking workspace contents...'
                sh 'ls -la'
                sh 'ls -la website || echo "website folder not found!"'
            }
        }

        stage("Cleanup") {
            steps {
                echo 'Cleaning up any old container...'
                sh '''
                    if [ "$(docker ps -aq -f name=$CONTAINER_NAME)" ]; then
                        docker rm -f $CONTAINER_NAME
                    fi
                '''
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "Building Docker image..."
                script {
                    docker.build("${IMAGE_NAME}:latest", ".")
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Running container from built image..."
                sh """
                    docker run -d \
                        --name $CONTAINER_NAME \
                        -p $HOST_PORT:$CONTAINER_PORT \
                        $IMAGE_NAME:latest
                """
            }
        }
    }

    post {
        always {
            echo "Pipeline completed!"
        }
    }
}
