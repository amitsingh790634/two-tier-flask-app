pipeline {
    agent any

    stages {
        stage('Code Clone') {
            steps {
                echo "🔄 Cloning repository..."
                git url: 'https://github.com/amitsingh790634/two-tier-flask-app.git', branch: 'main'
            }
        }

          stage('Build') {
            steps {
                sh 'docker build -t two-tier-flask-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Developer / Tester tests likh ke dega...'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHub',
                    usernameVariable: 'DOCKER_HUB_USER',
                    passwordVariable: 'DOCKER_HUB_PASSWORD'
                )]) {
                    sh 'docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASSWORD'
                    sh "docker image tag two-tier-flask-app $DOCKER_HUB_USER/two-tier-flask-app"
                    sh "docker push $DOCKER_HUB_USER/two-tier-flask-app:latest"
                }
            }
        }
       
        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
    }
}
