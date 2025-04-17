pipeline {
    agent { label "dev-server"}
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/sankyd/node-todo-cicd.git", branch:"sankyd-patch-2"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-new ."
                echo 'code build bhi ho gaya euuu'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhubcreds",
                passwordVariable:"dockerHubPass",
                usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag node-app-new:latest ${env.dockerHubUser}/node-app-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-new:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose down && docker compose up -d --build"
                echo 'deployment ho gayi'
            }
        }
    }
}
