pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building SOAPService...'
                    if (isUnix()) {
                        sh 'dotnet build SOAPService.sln'
                    } else {
                        bat 'dotnet build SOAPService.sln'
                    }
                    
                    echo 'Building RESTApi...'
                    if (isUnix()) {
                        sh 'dotnet build RESTApi.sln'
                    } else {
                        bat 'dotnet build RESTApi.sln'
                    }
                    
                    echo 'Building GrpcService...'
                    if (isUnix()) {
                        sh 'dotnet build GrpcService.sln'
                    } else {
                        bat 'dotnet build GrpcService.sln'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    if (isUnix()) {
                        sh 'dotnet test'
                    } else {
                        bat 'dotnet test'
                    }
                }
            }
        }
        
        stage('Docker Build') {
            steps {
                script {
                    echo 'Building Docker images...'
                    if (isUnix()) {
                        sh 'docker-compose build'
                    } else {
                        bat 'docker-compose build'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying containers...'
                    if (isUnix()) {
                        sh 'docker-compose up -d'
                    } else {
                        bat 'docker-compose up -d'
                    }
                }
            }
        }
    }
}