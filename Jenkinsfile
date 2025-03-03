pipeline{
    agent any 
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Umarsharief-07/ansible-docker-jenkins.git']])

            }
        }
        stage('docker image remove ') {
            steps {
                sh "sudo chmod 777 /var/run/docker.sock"
                script {
                
                def imageId = sh(script: "docker images -q ansible/jenkins/docker:latest", returnStdout: true).trim()
                    if (imageId) {
                        // echo "Image ${DOC_IMG}:latest found. Tagging and removing the image."
                        sh "docker tag ansible/jenkins/docker:latest"
                        
                        sh "docker rmi -f ansible/jenkins/docker:latest"
                    } else {
                        echo "Image ansible/jenkins/docker:latest:latest not found, skipping tag and remove."
                    }
        
                }

            }
        }
        stage('Docker build and run') {
            steps{
                sh "docker build -t ansible/jenkins/docker:${BUILD_NUMBER} ."
                sh "docker stop ansible && docker rm  ansible"
                sh "docker run -d --name ansible -p 3000:5000 ansible/jenkins/docker:${BUILD_NUMBER}"
                
            }
            
        }
    }
}
