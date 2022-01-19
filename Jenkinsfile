pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages{
        stage("Maven Build"){
            when {
                branch "develop"
            }
            steps{
               sh "mvn package"
            }
        }
        stage("SonarQube Analysis"){
            when {
                branch "develop"
            }
            steps{
               withSonarQubeEnv('sonar7') {
                    sh "mvn sonar:sonar"
               }
            }
        }
        stage("SonarQube Status"){
            when {
                branch "develop"
            }
            steps{
               timeout(time: 1, unit: 'HOURS') {
                //    For this to work, we should add webhook in sonar
                //    http://172.31.3.50:8080/sonarqube-webhook/
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                }
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