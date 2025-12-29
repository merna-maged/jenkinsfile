pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "merna123/hello-app"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/merna-maged/jenkinsfile-repo.git',
                    credentialsId: 'github'
            }
        }

        stage('Run Hello World') {
            steps {
                sh 'ls -l'
                sh 'chmod +x hello.sh'
                sh './hello.sh'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push ${DOCKER_IMAGE}:${DOCKER_TAG}
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully & Docker image pushed 🚀'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}
