pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Portfolio'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t portfolio-devops .'
            }
        }
    }
}
