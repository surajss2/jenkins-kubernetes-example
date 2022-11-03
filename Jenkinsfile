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
        stage("copy the manifest file on Ansible server"){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -avh /var/lib/jenkins/workspace/docker-k8-PipelineProject/*.yaml  root@192.168.30.138:/opt', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        } 
        stage("Run the playbook file"){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible_server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /opt/ansibleK8s.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }                          
                        
    }
    
}
