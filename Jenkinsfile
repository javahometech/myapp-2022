pipeline{
    agent any
    stages{
        stage("Maven Build"){
            when {
                branch "develop"
            }
            steps{
               sh "mvn package"
            }
        }
       stage("Deploy To dev"){
            when {
                branch "develop"
            }
            steps{
               echo "deploying to development server...."
            }
        }
        stage("Deploy To production"){
            when {
                branch "master"
            }
            steps{
               echo "deploying to master server...."
            }
        }
    }
}
