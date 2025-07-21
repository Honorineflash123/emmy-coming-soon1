pipeline {
    agent any

    triggers {
        pollSCM 'H/5 * * * *'
    }

    environment {
        CI = false
        SONARSCANNER = "sonarscanner"
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Inject Sonar token from Jenkins credentials
    }

    stages {
        stage('Run SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarscanner') {
                    script {
                        sh """
                            ${SONARSCANNER} \
                            -Dsonar.projectKey=qr-momo \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=${SONAR_TOKEN}
                        """
                    }
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Installing Dependencies and Building'
                sh 'docker build emmy-coming-soon1:${BUILD_NUMBER} .'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Deploying to Dockerhub'
                sh 'docker tag emmy-coming-soon1:${BUILD_NUMBER} Honorineflash123/emmy-coming-soon1-1'
                sh 'docker login -u ${USERNAME} -p ${PASSWORD} docker.io'
                sh 'docker push Honorineflash/emmy-coming-soon1-1'
            }
        }
    }
}
