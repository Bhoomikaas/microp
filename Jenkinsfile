pipeline{
    agent any
    tools{
        jdk "java-11"
        maven "maven"
    }
    stages{
        stage('Git-Checkout'){
            steps{
                git branch: 'main', url: ''
        }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('package'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('docker build'){
            steps{
                docker build -t bhoomikaas/app .
            }
        }
        stage('containerization'){
            steps{
                sh ...
                docker run -it -d --name c1 -p 9000:80 bhoomikaas/app .
                ...
            }
        }
        stage('Login to Docker Hub')
        {
            steps{
                script{
                    withCredential([usernamePassword(CredentialId: 'docker-hub-credntial', username Variable: 'DOCKER_USERNAME', 
                    sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin")])
                }
            }
            }
            }
            stage('pushing image to repository'){
                steps{
                    sh 'docker push bhoomikaas/app'
                }
            }     
    }
}
