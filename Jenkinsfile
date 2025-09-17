pipeline {
    agent any
    environment {
        dockerImage = "suryaraj/devops-evening67-new-app"
    }
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
                sh 'docker image build -t "${dockerImage}":"${BUILD_NUMBER}" .'
            }
        }
        stage('Scan docker image') {
            steps {
                echo 'Scanning docker image'
               // sh 'trivy image --timeout 10m --scanners vuln --exit-code 1 --severity HIGH,CRITICAL --ignore-unfixed "${dockerImage}":$BUILD_NUMBER'
            }
        }
        stage('Push Scanned Image to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-cred', url: '']) {
                    sh '''
                    docker push $dockerImage:$BUILD_NUMBER
                    '''
                }
            }
        }
        stage('Deploy Dev Instance') {
            steps {
                echo 'Deploying to Dev env.'
                sh 'docker container rm -f java-app-dev-instance || true'
                sh 'docker run -d -p 8082:8080 --name java-app-dev-instance ${dockerImage}:${BUILD_NUMBER}'
            }
        }
        stage('Deploy Production instance'){
            steps {
                timeout(time:1, unit:'HOURS'){
                input message:'Approve PRODUCTION Deployment?'
                }
                echo 'Deploying to Prod env.'
                sh 'docker container rm -f java-app-prod-instance || true'
                sh 'docker run -d -p 8083:8080 --name java-app-prod-instance ${dockerImage}:${BUILD_NUMBER}'
            }
        }
    }
    post { 
        always { 
            echo 'This is printed from always in post build!'
        }
    }
}

