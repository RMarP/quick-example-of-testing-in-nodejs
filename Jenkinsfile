pipeline {
    agent any
    tools {
        nodejs 'Node'
    }
    triggers {
        pollSCM '* * * * *'
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out.."
                git '''
                clone https://github.com/RMarP/quick-example-of-testing-in-nodejs.git
                '''
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                npm i
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                npm test
                '''
            }
        }
    }
}