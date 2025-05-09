pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Running build...'
                sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './test.sh'
            }
        }
    }
}
