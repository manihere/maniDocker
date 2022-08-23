pipeline{
    agent any
    stages{
        stage("Package Artifact")
         {
            steps{
                sh 'mvn -f java-tomcat-sample/pom.xml clean package' 
            }
        post{
            success{
                echo "Archiving artifacts"
                archiveArtifacts artifacts: "**/*.war"
                    }
            }
         }
        stage('Deploy to Staging'){
            steps{
            build job : 'DeploytoTomcat'
            }
        }

        stage('Deploy to Production'){
            steps{
                timeout (time:5, unit:'DAYS'){
                input message: "Approve Deploy to Production?"
                }
            build job : 'TomcatProd'
            }
        }

    }
}
