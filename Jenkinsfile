pipeline {
    agent any
    environment {
        GIT_BRANCH_NAME = 'prueba'  // Definición de la variable para el nombre de la rama
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
                    sh "git checkout ${GIT_BRANCH_NAME}"  // Cambio a la rama deseada
                    sh 'git pull origin ${GIT_BRANCH_NAME}'  // Asegurar que la rama local esté actualizada con la remota
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
