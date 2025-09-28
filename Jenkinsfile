pipeline {
    agent any

    tools {
        maven 'test-maven'
    }

    environment {
        name = "Sunil"
    }

    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package'
                echo "Hello %name%"
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }


}