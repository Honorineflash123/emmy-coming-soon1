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
           withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                echo 'Deploying to Dockerhub'
                sh 'docker tag -t emmy-coming-soon1:${BUILD_NUMBER} hnorinewehpon/emmy-coming-soon1:${BUILD_NUMBER}'
                sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                sh 'docker push hnorinewehpon/emmy-coming-soon1:${BUILD_NUMBER}'
           }
         }
       }
   }
}
