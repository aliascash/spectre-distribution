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
        SPECTRECOIN_RELEASE = "v2.0.6"
    }
    stages {
        stage('Latest binary archives') {
            when {
                anyOf { branch 'develop'; branch "${BRANCH_TO_DEPLOY}" }
            }
            parallel {
                stage('Debian') {
                    agent {
                        label "docker"
                    }
                    steps {
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Debian/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-debian",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_REPOSITORY=spectre-distribution ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./CentOS/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-centos",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_REPOSITORY=spectre-distribution ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Fedora/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-fedora",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_REPOSITORY=spectre-distribution ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./RaspberryPi/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-raspi",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_REPOSITORY=spectre-distribution ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Ubuntu/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-ubuntu",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_REPOSITORY=spectre-distribution ."
                            )
                            sh "rm Dockerfile"
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
        stage('Release binary archives') {
            when {
                branch 'master'
            }
            parallel {
                stage('Debian') {
                    agent {
                        label "docker"
                    }
                    steps {
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Debian/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-debian",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./CentOS/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-centos",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Fedora/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-fedora",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./RaspberryPi/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-raspi",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} ."
                            )
                            sh "rm Dockerfile"
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
                        script {
                            // Copy step on Dockerfile is not working if Dockerfile is not located on root dir!
                            // So copy required Dockerfile to root dir for each build
                            sh "cp ./Ubuntu/binary/Dockerfile ."
                            docker.build(
                                    "spectreproject/spectre-distribution-ubuntu",
                                    "--rm --build-arg GITHUB_TOKEN=${GITHUB_TOKEN} ."
                            )
                            sh "rm Dockerfile"
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
}