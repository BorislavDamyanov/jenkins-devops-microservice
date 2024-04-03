 pipeline {
    agent any
	stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                echo 'Building..'
                echo "$PATH"
                echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
                echo "BUILD_ID: ${env.BUILD_ID}"
                echo "BUILD_DISPLAY_NAME: ${env.BUILD_DISPLAY_NAME}"
                echo "JOB_NAME: ${env.JOB_NAME}"
                echo "JOB_BASE_NAME: ${env.JOB_BASE_NAME}"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post{
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
