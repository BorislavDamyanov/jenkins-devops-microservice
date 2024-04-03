 pipeline {
    agent any
    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"
    }
	stages {
        stage('Checkout') {
            steps {
                sh 'mvn --version'
                sh 'docker --version'
                echo 'Building..'
                echo "$PATH"
                echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
                echo "BUILD_ID: ${env.BUILD_ID}"
                echo "BUILD_DISPLAY_NAME: ${env.BUILD_DISPLAY_NAME}"
                echo "JOB_NAME: ${env.JOB_NAME}"
                echo "JOB_BASE_NAME: ${env.JOB_BASE_NAME}"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
         stage('Package') {
                    steps {
                       script {
                            sh 'mvn clean package -DskipTests'
                       }
                    }
                }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("boris1030/currency-exchange-devops:${env.BUILD_TAG}")
                }
            }
        }
        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                }
            }
        }
    }

}
