pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }

        stage('Restore dependencies') {
            steps {
                bat "dotnet restore"
            }
        }
        stage('Build project') {
            steps {
                bat "dotnet build --no-restore"
            }
        }
        stage('Test project') {
            steps {
                bat "dotnet test --no-build --verbosity normal"
            }
        }
    }
}
