pipeline{
    agent any
    tools{
        maven 'Maven-3.8.7'
    }
    stages{
        stage('Checkout'){
            steps{
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: 'ab9f859a-3f40-4b92-befa-35c110434084', url: 'https://github.com/PMFayazAhmed/corelogic.git']])
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package -f pom.xml'  
            }
        }
        stage('Deploy war'){
            steps{
              deploy adapters: [tomcat9(credentialsId: '2e266ef9-5235-4067-887f-5792cc3703d5', path: '', url: 'http://35.230.33.36:8090/')], contextPath: null, war: '**/*.war'  
            }
        }
        stage('Upload to Nexust'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/PollSCM-Corelogic.war', type: 'war']], credentialsId: 'cf9a36d1-6c9f-4cad-afb5-da810f47a344', groupId: 'com.adaequare', nexusUrl: '35.199.182.20:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
    }
}
