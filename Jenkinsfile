pipeline {
    agent any

    stages {
        stage('Checkout'){
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'df36754e-1202-4f00-8bd4-1bb529000ffb', url: 'https://github.com/deelakar/Task-6.1C.git']])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Stage 1: Build'
                    echo 'Build the code using a build automation tool to compile and package the code.'
                    echo 'Tool: Maven'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Stage 2: Unit and Integration Tests'
                    echo 'Run unit tests to ensure the code functions as expected and run integration tests to ensure different components of the application work together as expected.'
                    echo 'Tool: JUnit , TestNG'
                }
            }
            post {
                success {
                    emailext(
                        to: 'jenkintestuser@gmail.com',
                        subject: "Unit and Integration Tests Successful - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The unit and integration tests stage was successful.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'jenkintestuser@gmail.com',
                        subject: "Unit and Integration Tests Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The unit and integration tests stage failed. Please check the logs to find the error.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Stage 3: Code Analysis'
                    echo 'Integrate a code analysis tool to analyze the code and ensure it meets industry standards.'
                    echo 'Tool: SonarQube'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Stage 4: Security Scan'
                    echo 'Perform a security scan on the code using a tool to identify any vulnerabilities.'
                    echo 'Tool: OWASP Dependency-Check'
                }
            }
            post {
                success {
                    emailext(
                        to: 'jenkintestuser@gmail.com',
                        subject: "Security Scan Successful - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The security scan stage was successful.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'jenkintestuser@gmail.com',
                        subject: "Security Scan Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The security scan stage failed. Please check the logs.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Stage 5: Deploy to Staging'
                    echo 'Deploy the application to a staging server.'
                    echo 'Tool: AWS CLI to deploy to AWS EC2 instance'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Stage 6: Integration Tests on Staging'
                    echo 'Run integration tests on staging environment to ensure the application functions as expected '
                    echo 'Tool: Selenium'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Stage 7: Deploy to Production'
                    echo 'Deploy the application to the production server.'
                    echo 'Tool: AWS CLI to deploy to AWS EC2 instance'
                }
            }
        }
    }

    post {
        failure {
            emailext(
                to: 'jenkintestuser@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Failed",
                body: "Something went wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}. Please check the logs.",
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'jenkintestuser@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Succeeded",
                body: "The build and deployment of ${env.JOB_NAME} #${env.BUILD_NUMBER} was successful.",
                attachLog: true
            )
        }
    }
}
