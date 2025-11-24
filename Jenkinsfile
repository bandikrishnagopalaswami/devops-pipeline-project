pipeline {
    agent {
        docker { image 'docker:20.10' }
    }

    environment {
        IMAGE = "gopal183/jenkins-devops:latest"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub',
                    usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE'
            }
        }

        stage('Deploy (Local)') {
            steps {
                sh 'echo "Deployment completed successfully!"'
            }
        }
    }
}
