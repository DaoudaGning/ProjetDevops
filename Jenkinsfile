pipeline {
    agent {label 'docker'}
    environment {
        JENKINS_PRED = credentials('jenkins_pred')
        DOCKERHUB_USER = "gning26"
        BACKEND_IMAGE = "gning26/backend:v1"
        FRONTEND_IMAGE = "gning26/frontend:v1"
    }
    stages {

        stage('Build Backend Image') {
            steps {
                script {
                    sh 'docker build -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    sh 'docker build -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Login vers DockerHub') {
            steps {
                sh 'echo $JENKINS_PRED | docker login -u $DOCKERHUB_USER --password-stdin'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $BACKEND_IMAGE'
                sh 'docker push $FRONTEND_IMAGE'
            }
        }

        stage('Docker build tag') {
            steps {
                script {
                    sh 'docker tag backend:v1 $BACKEND_IMAGE'
                    sh 'docker tag frontend:v1 $FRONTEND_IMAGE'
                }
            }
        }
        
    }
}