pipeline {
    agent any

    environment {
        IMAGE_NAME = 'static-web-app'
        CONTAINER_NAME = 'static-web-test'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         git 'https://github.com/your-username/your-repo.git' // Already cloned, so skipping
        //     }
        // }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest", ".")
                }
            }
        }

        stage('Run Container (Test)') {
            steps {
                script {
                    // Stop and remove container if it exists
                    sh """
                    if [ \$(docker ps -aq -f name=${CONTAINER_NAME}) ]; then
                        docker rm -f ${CONTAINER_NAME}
                    fi
                    """

                    // Run container mapping port 8081 to 80 inside container
                    dockerImage.run("-d -p 8081:80 --name ${CONTAINER_NAME}")
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Add your deployment steps here'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh """
            if [ \$(docker ps -aq -f name=${CONTAINER_NAME}) ]; then
                docker rm -f ${CONTAINER_NAME}
            fi
            """
        }
    }
}
