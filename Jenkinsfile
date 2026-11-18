pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'test -s index.html'
                sh 'grep -q "Welcome to Student Management" index.html'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'index.html', fingerprint: true
        }
    }
}
