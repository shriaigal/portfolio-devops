pipeline {
agent any

```
environment {
    AWS_REGION = 'ap-south-1'
    ECR_REPO = '880252975320.dkr.ecr.ap-south-1.amazonaws.com/portfolio'
}

stages {

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t portfolio:v1 .'
        }
    }

    stage('Login to ECR') {
        steps {
            sh '''
            aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 880252975320.dkr.ecr.ap-south-1.amazonaws.com
            '''
        }
    }

    stage('Tag Image') {
        steps {
            sh 'docker tag portfolio:v1 880252975320.dkr.ecr.ap-south-1.amazonaws.com/portfolio:v1'
        }
    }

    stage('Push Image') {
        steps {
            sh 'docker push 880252975320.dkr.ecr.ap-south-1.amazonaws.com/portfolio:v1'
        }
    }
}

post {
    success {
        echo 'Docker Image Successfully Pushed to ECR'
    }

    failure {
        echo 'Pipeline Failed'
    }
}
```

}
