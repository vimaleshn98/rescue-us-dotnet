pipeline {
    agent any

    environment {
        REGISTRY = 'vimalesh198' // Docker registry username
        SEARCH_IMAGE_NAME = 'dotnet_animal_rescue-search-service'
        ANIMAL_IMAGE_NAME = 'dotnet_animal_rescue-animal-service'
        IMAGE_TAG = 'latest'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         git url: 'https://github.com/vimaleshn98/rescue-us-dotnet.git', branch: 'main'
        //     }
        // }
        
        // stage("Parallel Build Services Asp animal rescue"){
        //     parallel {
        //         stage("Build Services Asp animal service"){
        //             agent {
        //                 docker {
        //                     image 'mcr.microsoft.com/dotnet/sdk:6.0' // Use the appropriate .NET SDK version
        //                     args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket if needed
        //                 }
        //             }

        //             steps{
        //                 dir("rescue-us-dotnet/Services/AnimalService") {
        //                     sh(script: 'dotnet build AnimalService.csproj --configuration Release')
        //                 }
        //             }
        //             post{
        //                 always{
        //                     echo(message: 'Build Services Asp stage ')
        //                 }
        //                 success{
        //                     echo(message: 'Build Services Asp successfull')
        //                 }
        //                 unsuccessful{
        //                     echo(message: 'Build Services Asp unsuccessfull')
        //                 }
        //             }
        //         }
        //         stage("Build Services Asp Search service"){
        //             agent {
        //                 docker {
        //                     image 'mcr.microsoft.com/dotnet/sdk:6.0' // Use the appropriate .NET SDK version
        //                     args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket if needed
        //                 }
        //             }
        //             steps{
        //                 dir("rescue-us-dotnet/Services/SearchService") {
        //                     sh(script: 'dotnet build SearchService.csproj --configuration Release')
        //                 }
        //             }
        //             post{
        //                 always{
        //                     echo(message: 'dotnet build stage ')
        //                 }
        //                 success{
        //                     echo(message: 'dotnet build successfull')
        //                 }
        //                 unsuccessful{
        //                     echo(message: 'dotnet build unsuccessfull')
        //                 }
        //             }
        //         }
        //     }
        // }


        // stage("Parallel Test Services Asp animal rescue"){
        //     parallel {
        //         stage("Test Services Asp animal service"){
        //             agent {
        //                 docker {
        //                     image 'mcr.microsoft.com/dotnet/sdk:6.0' // Use the appropriate .NET SDK version
        //                     args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket if needed
        //                 }
        //             }

        //             steps{
        //                 dir("rescue-us-dotnet/Services/AnimalService") {
        //                     sh(script: 'dotnet Test AnimalService.csproj --configuration Release')
        //                 }
        //             }
        //             post{
        //                 always{
        //                     echo(message: 'Test Services Asp stage ')
        //                 }
        //                 success{
        //                     echo(message: 'Test Services Asp successfull')
        //                 }
        //                 unsuccessful{
        //                     echo(message: 'Test Services Asp unsuccessfull')
        //                 }
        //             }
        //         }
        //         stage("Test Services Asp Search service"){
        //             agent {
        //                 docker {
        //                     image 'mcr.microsoft.com/dotnet/sdk:6.0' // Use the appropriate .NET SDK version
        //                     args '-v /var/run/docker.sock:/var/run/docker.sock' // Mount Docker socket if needed
        //                 }
        //             }
        //             steps{
        //                 dir("rescue-us-dotnet/Services/SearchService") {
        //                     sh(script: 'dotnet Test SearchService.csproj --configuration Release')
        //                 }
        //             }
        //             post{
        //                 always{
        //                     echo(message: 'dotnet Test stage ')
        //                 }
        //                 success{
        //                     echo(message: 'dotnet Test successfull')
        //                 }
        //                 unsuccessful{
        //                     echo(message: 'dotnet Test unsuccessfull')
        //                 }
        //             }
        //         }
        //     }
        // }


        // sudo curl -L "https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
        // sudo chmod +x /usr/local/bin/docker-compose
        // docker-compose --version

        stage('Build and Push Docker Image') {
            steps {
                script {
                    def userInput = input message: 'Do you want to proceed?', parameters: [
                                booleanParam(defaultValue: false, description: 'Push to dotnet animal rescue project to Docker Hub?', name: 'Push')
                            ]
                    // Build and push the Docker image
                    sh 'docker-compose build'
                    sh "docker tag ${SEARCH_IMAGE_NAME}:${IMAGE_TAG} ${REGISTRY}/${SEARCH_IMAGE_NAME}:${IMAGE_TAG}"
                    sh "docker tag ${ANIMAL_IMAGE_NAME}:${IMAGE_TAG} ${REGISTRY}/${ANIMAL_IMAGE_NAME}:${IMAGE_TAG}"
                    withDockerRegistry(credentialsId: 'docker', url: 'https://index.docker.io/v1/') {
                        sh "docker push ${REGISTRY}/${SEARCH_IMAGE_NAME}:${IMAGE_TAG}"
                        sh "docker push ${REGISTRY}/${ANIMAL_IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }

        // stage('Deploy with Docker Compose') {
        //     steps {
        //         script {
        //             // Deploy using docker-compose
        //             sh 'docker-compose up -d'
        //         }
        //     }
        // }
    }
}
