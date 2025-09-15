pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                echo 'Compiling source code'
                sh 'mvn -f pom.xml clean compile'
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
                sh 'mvn -f pom.xml package'
            }
            post {
                success {
                    echo "Build success, archiving the artifact"
                    archiveArtifacts artifacts: '**/*.war'

                }
            }
        }
        stage('Create docker image') {
            steps {
                echo 'Creating docker image'
                sh 'docker image build -t myapp.local/javaapp:"${BUILD_NUMBER}" .'
            }
        }
    }
}

