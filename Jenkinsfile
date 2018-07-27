pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                git url: "git@github.com:korekontrol/packer-debian9.git"
            }
        }
        stage("build") {
            steps {
                sh "packer build debian-9-stretch-virtualbox.json"
            }
        }
        stage("publish") {
            steps {
                sh 'set +x && ' +
                    '. /opt/jenkins-go-env.sh && ' +
                    'export GITHUB_USER="korekontrol" && ' +
                    'export GITHUB_REPO="packer-debian9" && ' +
                    'set -x && ' +
                    "export TAG=\"ci-${env.BUILD_NUMBER}\" && " +
                    'github-release release --tag "${TAG}" --description "Automated build: ${TAG}" && ' +
                    'github-release upload --tag "${TAG}" --name *.box --file *.box'
            }
        }       
        stage("cleanup") {
            steps {
                sh 'rm -f *.box'
            }
        }
    }
}
