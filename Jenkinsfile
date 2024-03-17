pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps(){
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/manishnegi007/jenkins-docker']])
                sh 'mvn clean install'
            }
        }
        stage("Build docker image"){
            steps(){
                script{
                    sh 'docker build -t manishnegidocker/jenkins-docker .'
                }
            }
        }
        stage("Push Image to Docker Hub"){
            steps(){
                script{
                    withCredentials([string(credentialsId: 'dockercred-pwd', variable: 'dockercredpwd')]) {
                    sh 'docker login -u manishnegidocker -p ${dockercredpwd}'
}
                    sh 'docker push manishnegidocker/jenkins-docker'

                }
            }
        }

    }
}