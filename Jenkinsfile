pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages{
        stage("Maven Build"){
            when { 
                expression{
                    env.BRANCH_NAME.equals("develop") ||
                    env.BRANCH_NAME.startsWith("feature")
                }
            }
            steps{
               sh "mvn package"
            }
        }
        stage("SonarQube"){
            when {
                expression{
                    env.BRANCH_NAME.equals("develop") ||
                    env.BRANCH_NAME.startsWith("feature")
                }
            }
            steps{
               echo "sonarqube analysis...."
            }
        }
        stage("Nexus"){
            when {
                branch "develop"
            }
            steps{
               echo "uploading artifacts to nexus...."
            }
        }
        stage("Deploy To QA"){
            when {
                branch "qa"
            }
            steps{
               echo "deploying to qa server...."
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