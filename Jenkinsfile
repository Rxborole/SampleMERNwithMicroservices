pipeline {
    agent { label 'linux-manik' }

    environment {
        AWS_REGION = 'ap-south-1'
        AWS_ACCOUNT_ID = '116715028929'

        FRONTEND_REPO = 'streaming-frontend'
        HELLO_REPO = 'streaming-hello-service'
        PROFILE_REPO = 'streaming-profile-service'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Rxborole/SampleMERNwithMicroservices.git'
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'docker build -t streaming-frontend .'
                }
            }
        }

        stage('Build Hello Service') {
            steps {
                dir('backend/helloService') {
                    sh 'docker build -t streaming-hello-service .'
                }
            }
        }

        stage('Build Profile Service') {
            steps {
                dir('backend/profileService') {
                    sh 'docker build -t streaming-profile-service .'
                }
            }
        }

        stage('Login to Amazon ECR') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-ecr'
                ]]) {

                    sh '''
                    aws ecr get-login-password --region $AWS_REGION | \
                    docker login \
                    --username AWS \
                    --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                    '''
                }
            }
        }

        stage('Tag Images') {
            steps {

                sh '''
                docker tag streaming-frontend:latest \
                $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest

                docker tag streaming-hello-service:latest \
                $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$HELLO_REPO:latest

                docker tag streaming-profile-service:latest \
                $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$PROFILE_REPO:latest
                '''
            }
        }

        stage('Push Images') {
            steps {

                sh '''
                docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$FRONTEND_REPO:latest

                docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$HELLO_REPO:latest

                docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$PROFILE_REPO:latest
                '''
            }
        }
    }

    post {

        always {
            sh 'docker image prune -f'
        }

        success {
            echo 'Images successfully pushed to Amazon ECR'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}