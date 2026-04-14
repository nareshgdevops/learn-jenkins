pipeline {
    agent any

    environment {
        CC = 'clang'
        jenkins_password = credentials('agent-ssh-key')
    }

    stages {
        stage('Stage1') {
            steps {
                echo 'First Stage'
                sh 'echo message'
                echo "Jenkins password $jenkins_password"
            }
        }
    }


    post {
        always {
            echo "Run Always"
        }
    }
}