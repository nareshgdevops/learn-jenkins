pipeline {
    agent any
    options {
       buildDiscarder(logRotator(numToKeepStr: '3'))
       timestamps()
    }
    parameters {
       string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

       text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

       booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

       choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

       password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    environment {
        CC = 'clang'
        DEPLOY_TO = 'production'
        jenkins_password = credentials('agent-ssh-key')
    }

    stages {
        stage('Stage1') {
            steps {
                echo 'First Stage'
                sh 'echo message'
                echo "Jenkins username ${jenkins_password_USR}"
                echo "Jenkins password ${jenkins_password_PSW}"
                echo "Parameter String is ${params.PERSON}"
//                echo "Parameter description is ${params.description}"
                echo "Parameter choice is ${params.CHOICE}" //Groovy access
                sh 'echo Parameter choice is ${CHOICE}' //Shell access
            }
        }
        stage('Stage2') {
                input {
                    message "Should we continue?"
                    ok "Yes, we should."
                    submitter "alice,bob"
                    parameters {
                        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                    }
                }
                steps {
                    echo "Hello, ${PERSON}, nice to meet you."
                }
        }

        stage('Stage for conditions') {
                when {
                    //branch 'main'
                    allOf {
                        environment name: 'DEPLOY_TO', value: 'production'
                    }
                }

                parallel {
                    stage('Branch A') {
                        agent {
                            label "for-branch-a"
                        }
                        steps {
                            echo "On Branch A"
                        }
                    }
                    stage('Branch B') {
                        agent {
                            label "for-branch-b"
                        }
                        steps {
                            echo "On Branch B"
                        }
                    }
                    stage('Branch C') {
                        agent {
                            label "for-branch-c"
                        }
                        stages {
                            stage('Nested 1') {
                                steps {
                                    echo "In stage Nested 1 within Branch C"
                                }
                            }
                            stage('Nested 2') {
                                steps {
                                    echo "In stage Nested 2 within Branch C"
                                }
                            }
                        }
                    }
                }
        }
    }

    post {
        always {
            echo "Run Always"
        }
    }
}