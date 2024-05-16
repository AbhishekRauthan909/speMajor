pipeline {
    agent any
    environment {
        GITHUB_REPO_URL = 'https://github.com/AbhishekRauthan909/scientific_calculator.git'
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout code from GitHub repository
                    git branch: 'main', url: "${env.GITHUB_REPO_URL}"
                }
            }
        }
        stage('Maven Build') {
                    steps {
                                    dir('./speBackend') {
                                        sh 'mvn clean install'
                                    }
                                }
                }
          stage('Build Docker Images') {
                    steps {
                        dir('./speBackend') {
                            sh 'docker build -t abhishekrauthan2023106/music-backend .'
                        }
                        dir('./speFrontend') {
                            sh 'docker build -t abhishekrauthan2023106/music-frontend .'
                        }
                    }
                }
        stage('Push Docker Images') {
            steps {
                script {
                    // Tag and push Docker image to Docker Hub
                    docker.withRegistry('', 'DockerHubCred') {
                                        sh 'docker push abhishekrauthan2023106/music-backend'
                                        sh 'docker push abhishekrauthan2023106/music-frontend'
                    }
                }
            }
        }
    }
}