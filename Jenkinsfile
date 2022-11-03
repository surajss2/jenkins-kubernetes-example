pipeline {
    agent any
   
    stages {
        stage('Building the Docker image') {
            steps {
                sh 'docker build -t suraj435/nodejsapp-1.0:v1 .'
            }
        }
        stage("Push the docker image to docker Hub"){
            steps {
                sh ' docker push suraj435/nodejsapp-1.0:v1'
            }
        }
        stage("deploying to k8s cluster"){
            steps{
                
                sh "scp nodejsapp.yaml root@192.168.30.128:/root"
                sh "ssh root@192.168.30.28 kubectl apply -f nodejsapp.yml"              
                
            }                    
        }
                
    }
    
}
