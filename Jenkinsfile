pipeline {
    agent any
    environment {
        // Define the DOCKER_IMAGE variable here, accessible throughout the pipeline
        DOCKER_IMAGE = 'hello-world-python:latest' 
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Ensure the Git repository URL is correct and accessible by your Jenkins agent
                git branch: 'main', url: 'https://github.com/gaurav2103/jenkins_docker_python_hello_world.git'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Check if Dockerfile exists in the workspace
                    if (fileExists('Dockerfile')) {
                        echo 'Dockerfile found. Building image...'
                        // Build the Docker image using the defined environment variable
                        sh "docker build -t ${env.DOCKER_IMAGE} ."
                    } else {
                        // If Dockerfile is not found, fail the pipeline
                        error "Dockerfile not found in the workspace. Please ensure it's in the root of your repository."
                    }
                }
            }
        }
        stage('Docker Run') {
            steps {
                echo 'Running Docker container...'
                // Run the Docker container and automatically remove it after exit (--rm)
                sh "docker run --rm ${env.DOCKER_IMAGE}"
            }
        }
    }
    post {
        // Actions to perform after the pipeline finishes, regardless of success or failure
        success {
            echo 'Docker pipeline completed successfully!'
        }
        failure {
            echo 'Docker pipeline failed.'
            // You can add more actions here, e.g., send notifications
        }
        always {
            // This block runs regardless of success or failure
            echo 'This will always run after the pipeline stages.'
        }
    }
}
