pipeline {
    agent any 

    stages {
        stage('Execute External Script') {
            steps {
                // Grant execution permissions to the script file
                sh 'chmod +x hello.sh'
                // Execute the shell script
                sh './hello.sh'
            }
        }
    }
}
