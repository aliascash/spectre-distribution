#!groovy

pipeline {
    agent {
        label 'docker'
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
            sh 'docker-gc'
        }
    }
}