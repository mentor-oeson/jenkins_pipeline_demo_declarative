pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Running build...'
                sh 'chmod +x build.sh'    // <-- This line fixes the permission
                sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }
}
