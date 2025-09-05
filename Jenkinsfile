pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                echo 'Compiling source code'
                sh 'date'
            }
        }
        stage('Unittest') {
            steps {
                echo 'Running unittest'
            }
        }
        stage('build app') {
            steps {
                echo 'packaging the app'
                sh 'date'
            }
        }
        stage('create docker image') {
            steps {
                echo 'creating docker image'
                sh 'date'
            }
        }
        stage('scan docker image') {
            steps {
                echo 'scanning docker images'
                sh 'date'
            }
        }
        stage('Push image') {
            steps {
                echo 'Push image to dokcer registry'
                sh 'date'
            }
        }
        stage('Archive artifact') {
            steps {
                echo 'Archiving artifact'
                sh 'date'
            }
        }
        stage('Deploy to dev env') {
            steps {
                echo 'deploying to dev env'
            }
        }
    }
}

