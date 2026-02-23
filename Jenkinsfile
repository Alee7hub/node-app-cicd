@Library('sl-node-app-cicd') _

def IMAGE_NAME = 'alikakavand/node-app-cicd'

pipeline {
    agent any
    tools {
        nodejs 'nodejs-25'
    }

    stages {
        stage('Increment Version') {
            steps {
                script {
                    incrementVersion('minor')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    test()
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    buildImage(IMAGE_NAME)
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    dockerLogin()
                    dockerPush(IMAGE_NAME)
                }
            }
        }
        stage('Commit Version Bump') {
            steps {
                script {
                    commitVersionBump('github.com/Alee7hub/node-app-cicd.git')
                }
            }
        }
    }
}