pipeline {
    agent any

    triggers {
        pollSCM('*/5 * * * *')
    }

    stages {

        stage('Unit Tests') {
            steps {
                sh '''npm install;
                      
                      '''
            }
        }
        stage('Deploy to Dev') {
            environment {
                OW_AUTH = credentials('API AUTH')
                OW_APIHOST = credentials('API HOST')
            }
                steps {
                   sh '''serverless deploy -v'''
                }
        }
        stage('Deploy to SIT') {
            environment {
                OW_AUTH = credentials('API AUTH')
                OW_APIHOST = credentials('API HOST')
            }
                steps {
                   sh '''serverless deploy -v'''
                }
        }
        stage('Deploy to Pre-Prod') {
            environment {
                OW_AUTH = credentials('API AUTH')
                OW_APIHOST = credentials('API HOST')
            }
                steps {
                   sh '''serverless deploy -v'''
                }
        }
        stage('Promotion') {
            steps {
                timeout(time: 1, unit:'DAYS') {
                    input 'Deploy to Production?'
                }
            }
        }
        stage('Deploy to Production') {
            environment {
                OW_AUTH = credentials('API AUTH')
                OW_APIHOST = credentials('API HOST')
            }
            steps {
               sh '''serverless deploy -v'''
            }
        }
    }
}
