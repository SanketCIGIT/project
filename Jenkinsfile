pipeline {

    agent any



    environment {

        DOCKER_IMAGE = "sanketcigit/nginx-app" 

        DOCKER_CREDENTIALS = "Ditiss@10" 

    }



    stages {

        stage('Checkout') {

            steps {

                checkout scm

            }

        }



        stage('Build Docker Image') {

            steps {

                script {

                    docker.build("IMAGE}:${BUILD_NUMBER}")

                }

            }

        }



        stage('Push Docker Image') {

            steps {

                script {

                    withDockerRegistry([credentialsId: DOCKER_CREDENTIALS, url: 'https://index.docker.io/v1/']) {

                        docker.image("${DOCKER_IMAGE}:${BUILD_NUMBER}").push()

                    }

                }

            }

        }

    }



    post {

        always {

            cleanWs()

        }

        success {

            echo "Docker image pushed successfully!"

        }

        failure {

            echo "Pipeline fails"
	}
    }
}
