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
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                   }
           
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
