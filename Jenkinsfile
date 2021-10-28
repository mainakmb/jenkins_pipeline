pipeline {
    
    agent any
    
    environment{
        dockerImage =''
        registry = 'mainakmb/pythonapp'
        registryCredential = 'dockerhub'
    }
    
    stages {
        stage('Checkout'){
        steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mainakmb/jenkins_pipeline.git']]])
        }
        }
        
        stage('Build Docker Image'){
            steps{
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage("Push Docker Image"){
            steps{
                script{
                    docker.withRegistry( '', registryCredential){
                    dockerImage.push()
                    }
                }
            }
        }
    }
}
