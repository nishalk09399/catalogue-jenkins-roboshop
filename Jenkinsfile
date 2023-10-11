//this pipeline is use to run the roboshop catalogue component

pipeline {
    agent { node { label 'AGENT-1' } }
    stages {
        stage('Install dependencies') {
            steps {
                sh 'ls -ltr'
                sh 'pwd'
                //sh 'npm install'
                echo "npm installed successfully"
            }
        }
        stage('Unit test') {
            steps {
                echo "unit testing is done here"
            }
        }
        //sonar-scanner command expect sonar-project.properties should be available
        // stage('Sonar Scan') {
        //     steps {
        //         sh 'ls -ltr'
        //         sh 'sonar-scanner'
        //     }
        // }

        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }
        stage('publish artifact'){
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '34.207.92.86:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.0',
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )  
            }
        }  
        stage('Deploy') {
            steps {
                echo "Deployment"
            }
        }
    }
    }
