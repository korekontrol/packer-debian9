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
    }
}
