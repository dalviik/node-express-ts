pipeline {
    agent { label 'node_slave_cow' }
    // agent any

    options {
        buildDiscarder(logRotator(daysToKeepStr: '5', numToKeepStr: '5', artifactNumToKeepStr: '5'))
        skipDefaultCheckout(true)
    }

    triggers {
        pollSCM('0 */1 * * 1-5')
    }

    environment {
        NEXUS_REGISTRY_URL = 'http://192.168.100.254:8081/repository/npm-server/'
        NEXUS_AUTH_TOKEN   = credentials('authwebexpress')
    }

    stages {
        stage('Pull code') {
            steps {
                cleanWs()
                checkout scm
            }
        }

        stage('Build') {
            steps {
                withGradle {
                    // sh 'chmod +x gradlew'
                    // sh 'echo hola'
                    sh 'pwd'
                    sh '''
                        ./gradlew -is registrySetup \
                                nodeSetup \
                                npmInstall \
                                npm_run_build \
                                -PregistryUrl=$NEXUS_REGISTRY_URL \
                                -PauthToken=$NEXUS_AUTH_TOKEN
                    '''
                }
            }
        }

        stage('Publish') {
            steps {
                withGradle {
                    sh '''
                        ./gradlew -is npm_publish
                    '''
                }
            }
        }
    }
}