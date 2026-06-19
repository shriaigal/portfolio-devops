pipeline {
agent any

```
environment {
    AWS_REGION = 'ap-south-1'
    ECR_REPO = '880252975320.dkr.ecr.ap-south-1.amazonaws.com/portfolio'
}

stages {

    stage('Clone Repository') {
        steps {
            git 'https://github.com/shriaigal/portfolio-devops.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t portfolio:v1 .'
        }
    }

    stage('Login to ECR') {
        steps {
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | \
                docker login --username AWS --password-stdin 880252975320.dkr.ecr.ap-south-1.amazonaws.com
                '''
            }
        }
    }

    stage('Tag Image') {
        steps {
            sh 'docker tag portfolio:v1 $ECR_REPO:v1'
        }
    }

    stage('Push Image') {
        steps {
            sh 'docker push $ECR_REPO:v1'
        }
    }
}
```

}
