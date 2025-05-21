pipeline {
    agent any
    
    tools{
        maven "Maven-3.9.9"
    }    

    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/Sivakoppala/Contact-Backend.git'
            }
        }
        stage('Maven Build'){
            steps{
             sh 'mvn clean package'
            }
        }
        stage('Docker Image'){
            steps{
             sh 'docker build -t sivakoppala/contact_backend_app .'
            }
        }
        stage('Docker Image push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u sivakoppala -p ${docker_pwd}'
                   sh 'docker push sivakoppala/contact_backend_app'
            }
            }
        }
        stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
