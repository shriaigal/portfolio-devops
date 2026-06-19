
at the top and bottom.

Your Jenkinsfile should start directly with:

:::writing{variant="document" id="48172"}
pipeline {
    agent any

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
}
:::

### Then Push Again

In VS Code terminal:

```bash
git add Jenkinsfile
git commit -m "Fixed Jenkinsfile syntax"
git push origin main