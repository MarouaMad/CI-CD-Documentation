pipeline {
    agent any

    tools {
        nodejs 'nodejs'
        dockerTool 'docker'
    }

    stages {
        stage("git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/MarouaMad/CI-CD-Documentation.git'
            }
        }

        stage("install dependencies") {
            agent {
                docker {
                    image 'node:lts-alpine3.17'
                    args '-v /var/run/docker.sock:/var/run/docker.sock --network devops_devops'
                }
            }
            steps {
                sh '''
                npm install
                npm run build
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def customImageTag = "my-image:v1"
                    sh "docker build -t ${customImageTag} ."
                }
            }
        }

        stage("SonarScanner") {
            agent {
                docker {
                    image 'sonarsource/sonar-scanner-cli'
                    args '-v /var/run/docker.sock:/var/run/docker.sock --network devops_devops'
                }
            }
            steps {
                sh '''
                curl http://sonarqube:9000 
                sonar-scanner \
                -Dsonar.projectKey=test \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://sonarqube:9000 \
                -Dsonar.login=admin \
                -Dsonar.password=sonar
                '''
            }
        }

        stage('run container') {
            steps {
                script {
                    def customImageTag = "my-image:v1"
                    sh "docker run -d -p9090:80 --name newcontainerjenkins ${customImageTag}"
                }
            }
        }
    }
}
