pipeline {
    agent any

    tools {
        maven 'test-maven'
    }

    environment {
        NAME = "Sunil"
    }

    parameters {
        string defaultValue: 'Sunil', description: 'Tell who are you?', name: 'LASTNAME'
    }


    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package'
                bat 'echo %NAME%'
                echo "Hello ${env.NAME}"
                echo "Hello ${params.LASTNAME}"
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }


}