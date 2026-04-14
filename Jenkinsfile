pipeline {
    agent any
    options {
       buildDiscarder(logRotator(numToKeepStr: '3'))
    }

    environment {
        CC = 'clang'
        jenkins_password = credentials('agent-ssh-key')
    }

    stages {
        stage('Stage1') {
            steps {
                echo 'First Stage'
                sh 'echo message'
                echo "Jenkins username ${jenkins_password_USR}"
                echo "Jenkins password ${jenkins_password_PSW}"
            }
        }
    }

    post {
        always {
            echo "Run Always"
        }
    }
}