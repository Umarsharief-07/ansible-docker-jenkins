pipeline{
    agent any 
    stages{
        stage("Checkout"){
            step{

            }
        }
        stage("docker build"){
            steps{
                def name = "ansible"

                sh """ 
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