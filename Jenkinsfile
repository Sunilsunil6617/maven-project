pipeline {
    agent any

    tools {
        maven 'test-maven'
    }

    environment {
        NAME = "Sunil"
    }

    parameters {
        string defaultValue: 'Agasthya', description: 'Tell who are you?', name: 'LASTNAME'
    }


    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package'
                bat 'echo %NAME%'
                echo "Hello ${env.NAME}"
                echo "Hello ${params.LASTNAME}"
            }

        }

        stage ('test') {
            parallel {
                stage('test 1') {
                    steps {
                        echo "Execute test 1"
                    }
                }

                stage('test 2') {
                    steps {
                        echo "Execute test 2"
                    }
                }
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }


}