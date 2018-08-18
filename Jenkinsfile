#!groovy

pipeline {
    agent {
        label 'docker'
    }
    environment {
        GITHUB_TOKEN = credentials('cdc81429-53c7-4521-81e9-83a7992bca76')
    }
    stages {
        stage ("Upload Debian binaries") {
            agent {
                dockerfile {
                    filename 'Debian/binary/Dockerfile'
                    reuseNode true
                    label 'temporary-uploader'
                    additionalBuildArgs  '--build-arg GITHUB_TOKEN=${GITHUB_TOKEN}'
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