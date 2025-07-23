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
                sh 'docker build -t emmy-coming-soon1:${IMAGE_NAME}:${BUILD_NUMBER} .'
         }
    }

       stage('Deployment') {
         steps {
        echo 'Deploying to Dockerhub'
        sh 'docker tag emmy-coming-soon1:${BUILD_NUMBER} yourdockerhubusername/emmy-coming-soon1:${BUILD_NUMBER}'
        sh 'docker push yourdockerhubusername/emmy-coming-soon1:${BUILD_NUMBER}'
        }
      }

       }
   }

