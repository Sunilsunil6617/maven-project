pipeline {
    agent any

    tools {
        maven  'maven version 3.9.11'
    }

    environment {
        NAME = "Sunil"
    }

    parameters {
        string defaultValue: 'Agasthya', description: 'Tell who are you?', name: 'LASTNAME'
        choice choices: ['dev', 'prod'], description: 'Selected env will used to deploy', name: 'ENV'
    }


    stages {
        stage ("Build") {
            steps {
                bat 'mvn clean package -DskipTests=true'
                // bat 'echo %NAME%'
                // echo "Hello ${env.NAME}"
                // echo "Hello ${params.LASTNAME}"
            }

        }

        stage ('test') {
            parallel {
                stage('test 1') {
                    steps {
                        echo "Execute test 1"
                        bat "mvn test"
                    }
                }

                stage('test 2') {
                    steps {
                        echo "Execute test 2"
                        bat "mvn test"
                    }
                }
            }

            post {
                // success {
                //     archiveArtifacts artifacts: '**/target/*.war'
                // }

                success {
                    dir("webapp/target/") {
                        stash name: "maven-build", includes: "*.war"
                    }
                }
            }
        }

        stage ('deploy to dev') {
            when {
                expression {
                    params.ENV == 'dev'
                }
                beforeAgent true
            }

            steps {
                dir("/var/www/html") {
                    unstash "maven-build"
                }
                bat """
                cd /var/www/html/
                jar -xvf webapp.war
                """
            }

        }

        stage ('deploy to prod') {
            when {
                expression {
                    params.ENV == 'prod'
                }
                beforeAgent true
            }

            steps {
                timeout(time: 5 unit:'DAYS') {
                   input message: 'Wanna deploy anyway?'
                }

                dir("/var/www/html") {
                    unstash "maven-build"
                }
                bat """
                cd /var/www/html/
                jar -xvf webapp.war
                """
            }

        }
    }


}