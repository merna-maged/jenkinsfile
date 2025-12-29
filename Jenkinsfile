pipeline {
    agent any

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
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
