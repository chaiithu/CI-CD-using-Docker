pipeline {
    agent any
    stages {
        stage ('scm') {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chaiithu/kotiproject12.git']])
                }
            }
        }
        stage ('image build and tag') {
            steps {
                script {
                    sh ''' docker build -t chaithu .
                           docker tag chaithu chaithuchaithanya/static-app:v1'''
                }
            }
        }
        stage ('push image') {
            steps {
                   withDockerRegistry(credentialsId: 'docker-cred', url: '') {
                        sh '''docker push chaithuchaithanya/static-app:v1'''
                }
            }
            }
        stage ('deploy to container') {
            steps {
                script {
                    sh '''docker run -d -p 80:80 --name poori chaithu'''
                }
            }
        }
        }
    }
            

    
