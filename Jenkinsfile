pipeline {
    agent { label 'ayush' }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ayush-bhoyar/Application-test.git'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u "$DOCKER_USER" -p "$DOCKER_PASS"'
                }
                sh 'docker build -t ayushdocker2607/testapp:latest .'
                sh 'docker push ayushdocker2607/testapp:latest'
            }
        }

        stage('Deploy from Docker Hub') {
            steps {
                sh 'docker stop testcontainer || true'
                sh 'docker rm testcontainer || true'
                sh 'docker pull ayushdocker2607/testapp:latest'
                sh 'docker run -d -p 3000:3000 --name testcontainer ayushdocker2607/testapp:latest'
            }
        }
    }
}
