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
            }
        }
    }
}
