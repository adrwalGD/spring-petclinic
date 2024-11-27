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
    }
}
