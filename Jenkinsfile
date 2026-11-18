pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Build') {
            steps {
                script {
                    if (!fileExists('index.html')) {
                        error 'index.html is missing'
                    }

                    if (!readFile('index.html').contains('Welcome to Student Management')) {
                        error 'The student management welcome message is missing'
                    }
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'index.html', fingerprint: true
        }
    }
}
