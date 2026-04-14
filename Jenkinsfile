pipeline {
    agent any

    environment {
        CC = 'clang'
        jenkins_password = credentials('agent-ssh-key')
    }

    stages {
        stage('Stage1') {
            steps {
                sh 'First Stage'
                sh 'echo "Jenkins user name is $jenkins_password"'
            }
        }
    }


    post {
        always {
            echo "Run Always"
        }
    }
}