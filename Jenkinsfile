pipeline {
    agent any
    environment {
        GITHUB_REPO_URL = 'https://github.com/AbhishekRauthan909/speMajor.git'
        MAVEN_HOME = '/opt/homebrew/opt/maven'

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
                                        sh "${env.MAVEN_HOME}/bin/mvn clean install"
                                    }
                                }
                }
          stage('Build Docker Images') {
                    steps {
                        dir('./speBackend') {
                                 docker.build('abhishekrauthan2023106/music-backend')
                        }
                        dir('./spe-frontend') {
                              docker.build('abhishekrauthan2023106/music-frontend')
}
                    }
                }
        stage('Push Docker Images') {
            steps {
                script {
                    // Tag and push Docker image to Docker Hub
                    docker.withRegistry('', 'DockerHubCred') {
                                         docker.image('abhishekrauthan2023106/music-backend').push('latest') 
                                        docker.image('abhishekrauthan2023106/music-frontend').push('latest') 
                    }
                }
            }
        }
    }
}
