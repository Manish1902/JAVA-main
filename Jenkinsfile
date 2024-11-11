pipeline {
    agent any

    tools {
        maven 'maven' // Assuming 'maven' is the name of the Maven installation in Jenkins
    }

    environment {
        TOMCAT_DEPLOY_PATH = 'C:\\Program Files\\Apache Software Foundation\\Tomcat 11 0_Tomcat11_Temp'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat "mvn test"
            }
        }

        stage('Build WAR') {
            steps {
                bat "mvn clean package -DskipTests"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Debugging step to print the paths
                    echo "Target WAR Path: target\\*.war"
                    echo "Tomcat Deployment Path: ${env.TOMCAT_DEPLOY_PATH}\\webapps\\"
                    // Proceed with the deployment
                    bat "copy \"C:\\Users\\ACER\\.jenkins\\workspace\\Maven-build\\target\\*.war\" \"${env.TOMCAT_DEPLOY_PATH}\\webapps\\""
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
