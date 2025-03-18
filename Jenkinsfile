@Library('jenkins-shared-library') _

pipeline {
    agent { label 'ayush' }

    environment {
        IMAGE_NAME = 'ayushdocker2607/testapp:v2'
        CONTAINER_NAME = 'testcontainer-1'
        PORT = '3000'
        DOCKER_CRED_ID = 'dockerhub-cred'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ayush-bhoyar/Application-test.git'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                buildAndPushDocker(env.IMAGE_NAME, env.DOCKER_CRED_ID)
            }
        }

        stage('Deploy from Docker Hub') {
            steps {
                deployDockerContainer(env.IMAGE_NAME, env.CONTAINER_NAME, env.PORT)
            }
        }
    }
}
