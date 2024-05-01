pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/oriyomi1976/node-todo-cicd.git", branch: "master"
                echo  'pull code successfully'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t oriyomi1976/node-app-test-new ."
                echo ' build docker image successfully'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning succesfil'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker tag oriyomi1976/node-app-test-new:latest oriyomi1976/node-app-test-new:latest"
                sh "docker push oriyomi1976/node-app-test-new:latest"
                echo 'image push succesfully'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment succesful'
            }
        }
    }
}
