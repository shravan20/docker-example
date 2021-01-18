pipeline {
    agent any

    environment {
                registry = "shravankb/ums-app"
                registryCredential = 'DockerHubCreds'
                dockerImage = ''
    }

    stages {
        stage('Basic Setup') {
            steps {
                echo 'Basic Setup and checks'
                sh 'node --version'
                sh 'npm --version'
                
                echo 'Install Project Dependencies'
                sh 'npm i'

            }
        }
        stage('Unit Testing') {
            steps {

                echo 'UMS Testing-in-Progress'
                sh 'npm run coverage'
            
            }
        }

        stage('SonarQube Scanner Analysis') {
            environment {
                scannerHome = tool 'sonar_scanner'
            }
            
            steps{
                echo 'Check Testing'

                withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }

            }
        }
// Todo: from here deployment part 

        stage('Build Docker Image'){
            
            steps{
             
             echo "Building Image"

                withEnv(["ENVIRONMENT=${NODE_ENV}", "PORT=${PORT}", "DBURI=${DBURL}"]){

                echo "Builing in process"
                echo "docker Check"
                sh "docker --version"
                echo "docker-compose Check"
                sh "docker-compose --version"

                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
                echo "Image built"
                }
            }

        }

        stage('Deploying Image to DockerHub'){
            
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Connect to Server'){
            sh 'ssh ec2'
        }


    }
}