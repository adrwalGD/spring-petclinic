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
                sh 'env'
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
                sh 'docker build -t adrwalgd/mr:$GIT_COMMIT .'
                sh 'docker push adrwalgd/mr:$GIT_COMMIT'
            }
        }
    }
}
