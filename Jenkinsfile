pipeline {
    agent any

    tools {
        maven 'test-maven'
    }

    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package'
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }


}