pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    environment {
        CI = false
        IMAGE_ENV = "dev"   // change to "prod" or "test" if needed
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Installing Dependencies and Building'
                sh 'docker build -t emmy-coming-soon1:${IMAGE_ENV}-${BUILD_NUMBER} .'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Deploying to Dockerhub'
                sh 'docker tag emmy-coming-soon1:${IMAGE_ENV}-${BUILD_NUMBER} hnorinewehpon/emmy-coming-soon1:${IMAGE_ENV}-${BUILD_NUMBER}'
                sh 'docker push hnorinewehpon/emmy-coming-soon1:${IMAGE_ENV}-${BUILD_NUMBER}'
            }
        }
    }
}
