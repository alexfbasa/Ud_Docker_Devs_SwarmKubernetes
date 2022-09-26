pipeline {
    environment {
        registry = "alexsimple/flask"
        registryCredential = 'dockerhub_id'
        dockerImage = 'flask'
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/alexfbasa/Ud_Docker_Devs_SwarmKubernetes.git'
            }
        }
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}