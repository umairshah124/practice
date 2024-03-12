pipeline {
    agent any
    stages {
        stage ('Build') {
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("umairshah379/mydockerrepo:1.1")
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/umairshah379/mydockerrepo/general', 'docker_credential') {
                        docker.image("umairshah379/mydockerrepo:1.1").push()
                        docker.image("umairshah379/mydockerrepo:1.1").push("latest")
                    }
                }
            }
        }
        stage('Deploy'){
            steps {
                sh "docker stop hello-world | true"
                sh "docker rm hello-world | true"
                sh "docker run --name hello-world -d -p 8080:8080 umairshah379/mydockerrepo:1.1"
            }
        }
    }

