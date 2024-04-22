pipeline {
    environment {
        registryCredential = 'docker'
        IMAGE_NAME = 'humnaarshad19/mlops_a1'
        TAG = 'latest' 
    }
    agent any
    stages {
        stage('Cloning Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/HumnaArshad19/mlops_A1.git'
            }
        }
        stage('Building our image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }
    }
    post {
        success {
            emailext(
                to: 'i202383@nu.edu.pk',
                subject: 'Build Successful ',
                body: 'The docker image successfully pushed to Dockerhub! Well Done!'
            )
        }
    }
}
