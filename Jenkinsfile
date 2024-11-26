pipeline {
    agent any
    environment {
        name = 'git-linux'
    }
    parameters {
        string(name: 'person', defaultValue: 'ubuntu', description: "Who are you?")
        booleanParam(name: 'isCentos', defaultValue: true, description: "Specify linux")
        choice(name: 'City', choices: ['Jaipur', 'Mumbai', 'Pune'], description: "Choose your city")
    }
    stages {
        stage('Run Commands') {
            steps {
                sh '''
                ls
                date
                pwd
                cal 2021
                '''
            }
        }
        stage('Environment Variables') {
            environment {
                username = 'myusername'
            }
            steps {
                sh 'echo "${BUILD_ID}"'
                sh 'echo "${name}"'
                sh 'echo "${username}"'
            }
        }
        stage('Parameters') {
            steps {
                echo 'Deploying on test environment'
                sh 'echo "${name}"'
                sh 'echo "${person}"'
            }
        }
        stage('Approval to Continue') {
            input {
                message "Should we continue to production?"
                ok "Proceed"
            }
            steps {
                echo 'Approval received, deploying to production'
            }
        }
        stage('Deploy on Production') {
            steps {
                echo 'Deployment to production started'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed!'
        }
        failure {
            echo 'Pipeline execution failed!'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
    }
}
