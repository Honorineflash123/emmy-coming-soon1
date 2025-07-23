pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    environment {
        CI = false
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Installing Dependencies and Building'
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
            }
     }

           stage('Deployment') {
            steps {
                echo 'Deploying to Dockerhub'
                sh 'docker tag -t emmy-coming-soon1:${BUILD_NUMBER} hnorinewehpon/emmy-coming-soon1-1'
                sh 'docker login -u ${USERNAME} -p ${PASSWORD} docker.io'
                sh 'docker push hnorinewehpon/emmy-coming-soon1-1'
                }
            }
        }
    }
}
