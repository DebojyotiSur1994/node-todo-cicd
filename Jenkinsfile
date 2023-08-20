pipeline {
    agent any
    stages{
        stage("code"){
            steps{
                git url: 'https://github.com/DebojyotiSur1994/node-todo-cicd.git', branch: 'master'
                echo "code has been cloned"
            }
        }
        stage("build"){
            steps{
                sh 'docker build . -t node-todo-app-cicd'
            }
        }
        stage("push to repo"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"pass",usernameVariable:"id")]){
                    sh "docker login -u ${env.id} -p ${env.pass}"
                    sh "docker tag node-todo-app ${env.id}/node-todo-app-cicd:latest"
                    sh "docker push ${env.id}/node-todo-app-cicd:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d --build"
            }
        }
    }
}
