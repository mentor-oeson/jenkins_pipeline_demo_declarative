pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR-USERNAME/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Running build script...'
                sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running test script...'
                sh './test.sh'
            }
        }
    }
}
