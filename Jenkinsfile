@Library("harilibs") _
pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'github-creds', url: 'https://github.com/javahometech/myapp-2022'
            }
        }
        stage("Maven Build"){
            steps{
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage(" Dev Tomcat Deploy"){
            steps{
                tomcatDeploy("172.31.1.213","ec2-user","tomcat-dev")
            }
        }
    }
}
