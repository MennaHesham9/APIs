pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building SOAPService...'
                    // Build SOAPService (located in SOAPService folder)
                    if (isUnix()) {
                        sh 'dotnet build SOAPService/SOAPService.sln'  // Using relative path for Unix
                    } else {
                        bat 'dotnet build SOAPService\\SOAPService.sln'  // Using relative path for Windows
                    }
                    
                    echo 'Building RESTApi...'
                    // Build RESTApi (use relative path if necessary)
                    if (isUnix()) {
                        sh 'dotnet build RESTApi/RESTApi.sln'  // Adjust path as needed
                    } else {
                        bat 'dotnet build RESTApi\\RESTApi.sln'  // Adjust path as needed
                    }
                    
                    echo 'Building GrpcService...'
                    // Build GrpcService (use relative path if necessary)
                    if (isUnix()) {
                        sh 'dotnet build GrpcService/GrpcService.sln'  // Adjust path as needed
                    } else {
                        bat 'dotnet build GrpcService\\GrpcService.sln'  // Adjust path as needed
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Running tests (make sure you're in the correct directory for tests)
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
                    // Build Docker images
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
                    // Deploy containers
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