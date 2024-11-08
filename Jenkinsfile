pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages {
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/axar12/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage ('Build docker image'){
            steps{
                script{
                   bat 'docker build -t akshar/devops-integration .'
                }
            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    bat 'docker login -u axar1201 -p ${dockerhubpwd}'
}
                    bat 'docker push akshar/devops-integration'
                }

            }
        }

    }
}