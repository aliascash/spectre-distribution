#!groovy

pipeline {
    agent any
    options {
        timestamps()
        timeout(time: 2, unit: 'HOURS')
//	ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '5'))
    }
    environment {
        // In case another branch beside master or develop should be deployed, enter it here
        BRANCH_TO_DEPLOY = 'xyz'
        GITHUB_TOKEN = credentials('cdc81429-53c7-4521-81e9-83a7992bca76')
    }
    stage('Build and upload image') {
        when {
            anyOf { branch 'develop'; branch 'master'; branch "${BRANCH_TO_DEPLOY}" }
        }
        parallel {
            stage('Debian') {
                agent {
                    label "docker"
                }
                steps {
                    dockerfile {
                        filename 'Debian/binary/Dockerfile'
                        reuseNode true
                        label 'temporary-uploader'
                        additionalBuildArgs '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
                    }
                }
                post {
                    always {
                        sh "docker system prune --all --force"
                    }
                }
            }
/*
            stage('CentOS') {
                agent {
                    label "docker"
                }
                steps {
                    dockerfile {
                        filename 'CentOS/binary/Dockerfile'
                        reuseNode true
                        label 'temporary-uploader'
                        additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
                    }
                }
                post {
                    always {
                        sh "docker system prune --all --force"
                    }
                }
            }
*/
            stage('Fedora') {
                agent {
                    label "docker"
                }
                steps {
                    dockerfile {
                        filename 'Fedora/binary/Dockerfile'
                        reuseNode true
                        label 'temporary-uploader'
                        additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
                    }
                }
                post {
                    always {
                        sh "docker system prune --all --force"
                    }
                }
            }
            stage('Raspberry Pi') {
                agent {
                    label "docker"
                }
                steps {
                    dockerfile {
                        filename 'RaspberryPi/binary/Dockerfile'
                        reuseNode true
                        label 'temporary-uploader'
                        additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
                    }
                }
                post {
                    always {
                        sh "docker system prune --all --force"
                    }
                }
            }
            stage('Ubuntu') {
                agent {
                    label "docker"
                }
                steps {
                    dockerfile {
                        filename 'Ubuntu/binary/Dockerfile'
                        reuseNode true
                        label 'temporary-uploader'
                        additionalBuildArgs '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
                    }
                }
                post {
                    always {
                        sh "docker system prune --all --force"
                    }
                }
            }
        }
    }
}
