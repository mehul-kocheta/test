pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/mehul-kocheta/test.git'
            }
        }

        stage('Build') {
            steps {
                // Replace with your build command
                echo 'Build'
            }
        }

        stage('Test') {
            steps {
                // Replace with your test command
                echo 'make test'
            }
        }

        stage('Deploy') {
            steps {
                // Replace with your deploy command
                echo 'make deploy'
            }
        }
    }

    post {
        success {
            // Notify success
            echo 'Build succeeded!'
        }
        failure {
            // Notify failure
            echo 'Build failed!'
        }
    }
}
