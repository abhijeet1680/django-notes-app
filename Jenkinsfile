@Library("Shared") _
pipeline {
    agent { label "vinod" }

    environment {
        PROJECT_NAME = 'notes-app'
        IMAGE_TAG = 'latest'
        DOCKERHUB_USER = 'abhighadge1994'
    }

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
                script {
                    clone("https://github.com/abhijeet1680/django-notes-app.git", "main")
                }
            }
        }

        stage("Build") {
            steps {
                script {
                    docker_build("${PROJECT_NAME}", "${IMAGE_TAG}", "${DOCKERHUB_USER}")
                }
            }
        }

        stage("Test") {
            steps {
                echo "Testing the code"
                // Add test steps here if needed
            }
        }

        stage("Push") {
            steps {
                script {
                    docker_push("${PROJECT_NAME}", "${IMAGE_TAG}", "${DOCKERHUB_USER}")
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the code"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
