pipeline {
    agent any
    environment {
        GIT_BRANCH_NAME = 'prueba'  // Definir la variable para el nombre de la rama
    }
    tools {
        nodejs 'Node'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out.."
                git url: 'https://github.com/RMarP/quick-example-of-testing-in-nodejs.git', branch: 'master'  // Checkout inicial en la rama principal (por ejemplo, 'master')
                script {
                    echo "Switching to branch ${GIT_BRANCH_NAME}"
                    def branchExists = sh(script: "git ls-remote --heads origin ${GIT_BRANCH_NAME}", returnStatus: true) == 0
                    if (branchExists) {
                        sh "git checkout ${GIT_BRANCH_NAME}"
                        sh "git pull origin ${GIT_BRANCH_NAME}"
                    } else {
                        error "Branch ${GIT_BRANCH_NAME} does not exist in the repository"
                    }
                }
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
