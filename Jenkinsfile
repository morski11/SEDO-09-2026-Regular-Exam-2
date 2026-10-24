pipeline {
    agent any

    stages {
        stage('Debug branch') {
            steps {
                echo "BRANCH_NAME = ${env.BRANCH_NAME}"
                echo "GIT_BRANCH = ${env.GIT_BRANCH}"
                echo "JOB_NAME = ${env.JOB_NAME}"

                bat 'git branch --show-current'
                bat 'git rev-parse --abbrev-ref HEAD'
            }
        }

        stage('Restore dependencies') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                bat 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
