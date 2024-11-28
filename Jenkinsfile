pipeline {
    agent {
        label 'docker'
    }
    tools {
        maven 'M3'
    }

    stages {
        stage('Checkstyle') {
            steps {
                sh 'mvn checkstyle:checkstyle'
                sh 'tar -czf checkstyle-result.tar.gz target/reports'
                archiveArtifacts artifacts: 'checkstyle-result.tar.gz', onlyIfSuccessful: true
            }
        }
        stage('Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build without tests') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    docker.build("adrwalgd/mr:$GIT_COMMIT")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        docker.image("adrwalgd/mr:$GIT_COMMIT").push()
                    }
                }
            }
        }
    }
}
