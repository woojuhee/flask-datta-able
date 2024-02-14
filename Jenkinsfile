pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Make build
                    sh 'make build'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials
                    withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_TOKEN', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}"
                    }
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    // Push image
                    sh 'make push'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
    }
}
