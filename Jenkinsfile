pipeline {
    agent any

    environment {
        IMAGE_NAME = 'static-web-app'
        CONTAINER_NAME = 'static-web-test'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         git 'https://github.com/mentor-oeson/jenkins_pipeline_demo_declarative.git'
        //     }
        // }

        stage('Build Docker Image') {
            steps {
                echo '🔨 Building Docker image...'
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest", ".")
                }
            }
        }

        stage('Run Container (Test)') {
            steps {
                echo '🚀 Running test container...'
                script {
                    sh """
                    if [ "\$(docker ps -aq -f name=${CONTAINER_NAME})" ]; then
                        echo "🧹 Removing existing container..."
                        docker rm -f ${CONTAINER_NAME}
                    fi
                    """
                    dockerImage.run("-d -p 8081:80 --name ${CONTAINER_NAME}")
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '📦 Deployment step placeholder (add your logic here)'
            }
        }
    }

    post {
        always {
            echo '🧼 Cleanup...'
            script {
                sh """
                if [ "\$(docker ps -aq -f name=${CONTAINER_NAME})" ]; then
                    docker rm -f ${CONTAINER_NAME}
                fi
                """
            }
        }
    }
}
