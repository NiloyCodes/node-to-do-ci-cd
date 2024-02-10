pipeline{
    agent { label "dev-server"}
    
    stages {
        
        stage("Code"){
            steps{
                git url: "https://github.com/LondheShubham153/node-todo-cicd.git", branch: "master"
                echo 'Code has been cloned'
            }
            
        }
        
        stage("Build"){
            steps{
                sh "docker build -t node-app-test-new ."
                echo 'Code has been build'
            }
            
        }
        
        stage("Push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                echo 'Code has been pushed'
                }
            }
            
        }
        
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Code has been deployed'
            }
            
        }
    }
}
