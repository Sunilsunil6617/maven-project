pipeline {
    agent any

    tools {
        maven 'test-maven'
    }

    environment {
        name = "Sunil"
    }

    parameters {
        string defaultValue: 'Sunil', description: 'Tell who are you?', name: 'Username'
    }


    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package'
                bat 'echo %name%'
                echo "Hello ${env.name}"
                echo "Hello ${params.username}"
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }


}