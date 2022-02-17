pipeline {
    agent any 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '7d45d4df-5f8a-49e0-af51-c0f629e77c4b', url: 'https://github.com/ThuyLam999/BooksUnitTest.git'
            }
        }
        
        stage('Restore packages'){
            steps{
                bat "dotnet restore WEBAPI/WEBAPI.csproj"
            }
        }

        stage('Clean'){
            steps{
                bat "dotnet clean WEBAPI/WEBAPI.csproj"
            }
        }

        stage('Build'){
            steps{
                bat "dotnet build WEBAPI/WEBAPI.csproj --configuration Release --no-restore"
            }
        }

        stage('Test: Unit Test'){
            steps {
                bat 'dotnet test TestProject/TestProject.csproj --configuration Release --no-restore'
            }
        }
       
        stage('Test: Integration Test'){
            steps {
                 echo 'Test: Integration Test'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        
        success {
            mail bcc: '', body: 'Build Success', cc: '', from: '', replyTo: '', subject: 'Test Run SUCCESSFUL', to: 'thanhthuyyasou234@gmail.com'
        }  

        failure {
            mail bcc: '', body: 'Build False', cc: '', from: '', replyTo: '', subject: 'Test Run FAILED', to: 'thanhthuyyasou234@gmail.com'
        }
    }
}
