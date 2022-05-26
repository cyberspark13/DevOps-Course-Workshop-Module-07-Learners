pipeline {
    agent none

    stages {
        stage('Build') {

            agent {
                docker {
                   image 'mcr.microsoft.com/dotnet/sdk:6.0'
                }
            }

            environment {
                DOTNET_CLI_HOME = '/tmp/DOTNET_CLI_HOME'
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('Test') {
            
            agent {
                docker {
                    image 'node:17-bullseye'
                }
            }
            
            steps {
                dir ('DotnetTemplate.Web/'){
                    sh 'npm install && npm run build && npm t && npm run lint'
                    }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}