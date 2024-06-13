pipeline {
    agent any
    tools {
        nodejs 'Node'
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out.."
                git url: 'https://github.com/RMarP/quick-example-of-testing-in-nodejs.git', branch: 'prueba'  // Checkout inicial en la rama principal (por ejemplo, 'master')
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                sh 'npm i'
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh 'npm test'
            }
        }
    }
}
