@Library("harilibs") _
pipeline{
    agent any
    stages{
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
