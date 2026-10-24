pipeline {
    agent any

    stages {

        stage('Restore dependencies') {
            when {
                expression { env.GIT_BRANCH == 'origin/main' }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                expression { env.GIT_BRANCH == 'origin/main' }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        } 

        stage('Test') {
            when {
                expression { env.GIT_BRANCH == 'origin/main' }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
