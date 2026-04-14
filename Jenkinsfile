pipeline {
    agent any

    stages {
        stage('Stage1') {
            steps {
                echo "First Stage"
            }
        }
    }


    post {
        always {
            echo "Run Always"
        }
    }
}