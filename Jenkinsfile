pipeline {
    agent { label 'node-agent' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Samhitha1598/Todo-code.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t trainwithshubham/Todo-code:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push trainwithshubham/Todo-code:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
