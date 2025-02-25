pipeline{
    agent any 
    stages {
        stage('Checkout') {
            step {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Umarsharief-07/ansible-docker-jenkins.git']])

            }
        }
        stage('docker build') {
            steps {
                script {

                def name = "ansible"

                sh """ 
                sudo usermod -aG docker ubuntu
                sudo chmod 777 /var/run/docker.sock
                docker build -t ansible/jenkins/docker:${BUILD_NUMBER} .

                if ["$name = "ansible"]; then
                   docker stop ansible && docker rm ansible
                else   
                   docker run -d --name ansible -p 4000:8080 ansible/jenkins/docker:${BUILD_NUMBER}
                fi
            """
                }

            }
        }
    }
}