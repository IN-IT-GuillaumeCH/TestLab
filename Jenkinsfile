pipeline {
   
    agent any

    stages {
        stage ('Get Code') {
            steps {
                checkout scm   
            }
        }

        stage ('Build') {
            steps {
                echo 'Build starting'
                sh 'cd lab-app'
                sh 'mvn -f lab-app/pom.xml -Dmaven.test.failure.ignore=true install'
                snDevOpsArtifact(artifactsPayload: """{"artifacts": [{"name": "labapp-web.jar", "version": "2.${currentBuild.number}.0","semanticVersion": "2.${currentBuild.number}.0","repositoryName": "ServiceNowLabAppRepo"}], "branchName": "main"}""")
                snDevOpsPackage(name: "lab-app-package", artifactsPayload: """{"artifacts":[{"name": "labapp-web.jar", "version": "2.${currentBuild.number}.0", "repositoryName": "ServiceNowLabAppRepo"}], "branchName": "main"}""")

                junit 'lab-app/target/surefire-reports/**/*.xml'
                echo 'Build ended'
            }
          }

        stage ('Deployment') {        
            steps {
                echo 'Deployment starting'
                
                echo 'Deployment ended'
            }
        }
    }
}
