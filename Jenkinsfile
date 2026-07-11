pipeline {
    agent { label 'linux-manik' }

    environment {
        AWS_REGION     = 'ap-south-1'
        AWS_ACCOUNT_ID = '116715028929'

        FRONTEND_REPO = 'streaming-frontend'
        HELLO_REPO    = 'streaming-hello-service'
        PROFILE_REPO  = 'streaming-profile-service'
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Rxborole/SampleMERNwithMicroservices.git'
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh '''
                    docker build -t streaming-frontend:latest .
                    '''
                }
            }
        }

        stage('Build Hello Service Image') {
            steps {
                dir('backend/helloService') {
                    sh '''
                    docker build -t streaming-hello-service:latest .
                    '''
                }
            }
        }

        stage('Build Profile Service Image') {
            steps {
                dir('backend/profileService') {
                    sh '''
                    docker build -t streaming-profile-service:latest .
                    '''
                }
            }
        }

        stage('Verify AWS Credentials') {
            steps {
                withCredentials([
                    [
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'aws-ecr'
                    ]
                ]) {

                    sh '''
                    echo "==============================="
                    echo "AWS Identity"
                    echo "==============================="

                    aws sts get-caller-identity

                    echo ""
                    echo "==============================="
                    echo "ECR Repositories"
                    echo "==============================="

                    aws ecr describe-repositories

                    echo ""
                    echo "==============================="
                    echo "AWS CLI Version"
                    echo "==============================="

                    aws --version
                    '''
                }
            }
        }

        stage('Login to Amazon ECR') {
            steps {
                withCredentials([
                    [
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'aws-ecr'
                    ]
                ]) {

                    sh '''
                    aws ecr get-login-password --region $AWS_REGION | \
                    docker login \
                    --username AWS \
                    --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
                    '''
                }
            }
        }

        stage('Tag Docker Images') {
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

        stage('Push Images to Amazon ECR') {
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

        success {

            echo '''
====================================
Pipeline Completed Successfully
====================================
'''
        }

        failure {

            echo '''
====================================
Pipeline Failed
====================================
'''
        }

        always {

            sh '''
            docker image prune -af || true
            docker builder prune -af || true
            '''
        }
    }
}
