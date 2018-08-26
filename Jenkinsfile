#!groovy

pipeline {
    agent {
        label 'docker'
    }
    environment {
        GITHUB_TOKEN = credentials('cdc81429-53c7-4521-81e9-83a7992bca76')
        SPECTRECOIN_RELEASE="2.0.6"
    }
    stages {
        stage ("Upload Debian binaries") {
            agent {
                dockerfile {
                    filename 'Debian/binary/Dockerfile'
                    reuseNode true
                    label 'temporary-uploader'
                    additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_RELEASE=${SPECTRECOIN_RELEASE}'
                }
            }
            steps {
                echo "Upload finished"
            }
        }
        stage ("Upload Ubuntu binaries") {
            agent {
                dockerfile {
                    filename 'Ubuntu/binary/Dockerfile'
                    reuseNode true
                    label 'temporary-uploader'
                    additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_RELEASE=${SPECTRECOIN_RELEASE}'
                }
            }
            steps {
                echo "Upload finished"
            }
        }
        stage ("Upload Fedora binaries") {
            agent {
                dockerfile {
                    filename 'Fedora/binary/Dockerfile'
                    reuseNode true
                    label 'temporary-uploader'
                    additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN} --build-arg SPECTRECOIN_RELEASE=${SPECTRECOIN_RELEASE}'
                }
            }
            steps {
                echo "Upload finished"
            }
        }
    }
    post {
        always {
            sh 'echo "todo: docker-gc"'
        }
    }
}