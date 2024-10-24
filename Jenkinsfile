pipeline{
    agent any
    tools{
        maven 'maven_3.9.9'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bsainath99/devops-integration']])
                bat 'mvn clean install'
            }
        }
        stage('build Docker Image'){
            steps{
                script{
                    bat 'docker build -t bsainath0099/devops-automation .'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-username-pwd', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                        bat 'docker login -u %DOCKERHUB_USER% -p %DOCKERHUB_PASS%'
                    }
                    bat 'docker push bsainath0099/devops-automation'
                }
            }
        }
    }
}