
pipeline {
    agent any

    // 1. Build Parameters
    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['DEV', 'QA', 'PROD'],
            description: 'Select deployment environment'
        )
    }

    // 2. Environment Variables
    environment {
        APP_NAME = 'my-java-app'
        DEPLOY_ENV = 'DEV'
    }

    stages {

        // 3. Checkout Stage
        stage('Checkout') {
            steps {
                echo 'Code checkout completed'
            }
        }

        // 4. Build Stage
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        // 5. Test Stage
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        // 6. Credentials Stage
        stage('Credentials Test') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'demo-secret',
                        variable: 'MY_SECRET'
                    )
                ]) {
                    sh 'echo "Credential loaded successfully"'
                    sh 'test -n "$MY_SECRET"'
                }
            }
        }

        // 7. Environment Details Stage
        stage('Environment Details') {
            steps {
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
                echo "Application: ${env.APP_NAME}"
                echo "Default Environment: ${env.DEPLOY_ENV}"
                echo "Selected Environment: ${params.ENVIRONMENT}"
            }
        }

        // 8. Deploy Stage
        stage('Deploy') {
            steps {
                echo "Selected environment: ${params.ENVIRONMENT}"
                echo "Deploying application to ${params.ENVIRONMENT}"
            }
        }
    }

    // 9. Post Build Actions
    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Please check the console output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
