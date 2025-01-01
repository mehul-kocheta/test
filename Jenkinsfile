pipeline {
    agent none

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_cred')
        DOCKERHUB_REPO = 'mehuljain4751/flask_server'
    }

    stages {
        stage('Build Docker Image and push') {
            agent {
                label 'amz-ec2'
            }
            steps {
                script {
                    git 'https://github.com/mehul-kocheta/flask_app.git'
                    dockerImage = docker.build("${env.DOCKERHUB_REPO}:${env.BUILD_NUMBER}")
                    docker.withRegistry('https://index.docker.io/v1/', 'docker_cred') {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            agent {
                label 'k8_node'
            }
            steps {
                script {
                    withCredentials([file(credentialsId: env.k8_cred, variable: 'KUBECONFIG')]) { 
                        sh 'kubectl run busybox --image=busybox --command -- sh -c "echo Hello Kubernetes! && sleep 3600"' 
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
        success {
            // Notify success
            echo 'Build, push, and deploy succeeded!'
        }
        failure {
            // Notify failure
            echo 'Build, push, or deploy failed!'
        }
    }
}
