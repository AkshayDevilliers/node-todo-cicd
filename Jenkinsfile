pipeline {
    agent any
    stages {
        stage("Code"){
            steps{
                git url: "https://github.com/AkshayDevilliers/node-todo-cicd.git", branch: "master"
                echo "code clone kiya hmne"
            }
        }
            stage("Build & Test") {
                steps{
                    sh "docker build -t node-app-test-new:latest ."
                    echo "build kar diya hmne"
                   
                }
            }
                stage("Push to Dockerhub") {
                    steps{
                         withCredentials([usernamePassword(credentialsId:"AkshayDocker", passwordVariable:"dockerHubKaPassword", usernameVariable:"merausername")]){
                        
            
                    sh "docker login -u ${env.merausername} -p ${env.dockerHubKaPassword}"
                    sh "docker tag node-app-test-new:latest ${env.merausername}/node-app-test-new:latest"
                    sh "docker push  ${env.merausername}/node-app-test-new:latest"
                    echo "push kiya image hmne"
                    }
                        echo "push ho gya"
                    }
                }
                    stage("Deploy") {
                        steps{
                            sh "docker-compose down && docker-compose up -d"
                            echo "deploy ho gya"
                        }
                    }
                
            
    }     
}
