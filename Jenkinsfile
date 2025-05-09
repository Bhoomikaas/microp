pipeline {
    agent any
    tools {
        jdk "java-11"
        maven "maven"
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Bhoomikaas/microp.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Docker Build') {
            steps {
                sh "docker build -t npic1.jfif}."
            }
        }
        stage('Containerization') {
            steps {
                sh "docker run -it -d --name c1 -p 9000:80 ${IMAGE_NAME}"
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }
        stage('Pushing Image to Repository') {
            steps {
                sh "docker push ${IMAGE_NAME}"
            }
        }
    }
}
