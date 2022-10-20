pipeline{
    agent any

    stages{

        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build ("k0dy/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script{
                    docker.withRegistry('https://resgistry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }

}
