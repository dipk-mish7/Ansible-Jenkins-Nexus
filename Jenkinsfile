pipeline {
       agent {
        label 'aws_ec2_ubuntu_label'
    }

    stages {
        stage('Clone') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/dipk-mish7/spring3hibernate.git'
            }
        }   
        stage('Integration and Unit Test') {
            steps {
                // Running Integration Test.
                sh 'mvn clean verify'
            }
        }
        stage('Packaging the Code') {
            steps {
                // Packaging the code 
                sh 'mvn package'
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '**/*.war', followSymlinks: false, onlyIfSuccessful: true
            nexusArtifactUploader artifacts: [[
            artifactId: 'Spring3HibernateApp', 
            classifier: '', 
            file: 'target/Spring3HibernateApp.war', 
            type: 'war']], 
            credentialsId: 'nexus', 
            groupId: 'Spring3HibernateApp', 
            nexusUrl: '52.66.186.101:8081', 
            nexusVersion: 'nexus3', 
            protocol: 'http', 
            repository: 'ninja-maven-release', 
            version: '4.0.0'
        }
    }
    
}
