pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\Yashwanth\\.kube\\config'
    }

    stages {
        stage('git') {
            steps {
                git 'https://github.com/yash1nthh/cicd1.git'
            }
        }

        stage('Build and Run Docker Image') {
            steps {
                bat 'docker build -t cicd .'
                bat 'docker run -dit --name containercicd -p 8040:80 cicd'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker login -u yash6422 -p Yash@64220204'
                bat 'docker tag cicd yash6422/cicd'
                bat 'docker push yash6422/cicd'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    bat '''
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                    '''
                }
            }
        }
    }
}
