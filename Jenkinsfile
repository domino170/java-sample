pipeline {
    agent any

    tools {
        maven 'JAVA_Maven'
    }

    stages {
        stage ('Build Servlet Project') {
            steps {
                /* Maven step */
                bat 'mvn clean package'
            }
            /*Post-build actions*/
            post {
                success {
                    echo 'Now Archiving...'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }


        stage ('Deploy Build in Production Environment') {
            steps {
                timeout (time: 5, unit: 'DAYS') {
                    input message : 'Approve PRODUCTION Deployment?'
                }

                build job : 'Prod_deployemnt'
            }

            post {
                success {
                    echo 'Deployment on PRODUCTION is Successful'
                }

                failure {
                    echo 'Deployment Failure on PRODUCTION'
                }
            }
        }
    }
}
