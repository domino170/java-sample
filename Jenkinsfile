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


        stage ('Deploy do Docker') {
            steps {
          cmd "docker build . -t javawebapp:${env.BUILD_ID}"
            }
        }
    }
}
