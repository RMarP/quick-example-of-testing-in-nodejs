pipeline {
    agent any
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
                git url: 'https://github.com/RMarP/quick-example-of-testing-in-nodejs.git'
            }
        }
        stage('Manage Branches') {
            steps {
                script {
                    def newBranch = 'new-branch'
                    def baseBranch = 'master'
                    
                    // Fetch all branches
                    sh 'git fetch --all'
                    
                    // Check if the new branch exists and delete it
                    def branchExists = sh(script: "git ls-remote --heads origin ${newBranch}", returnStatus: true) == 0
                    if (branchExists) {
                        echo "Deleting existing branch ${newBranch}"
                        sh """
                            git push origin --delete ${newBranch}
                            git branch -d ${newBranch}
                        """
                    }
                    
                    // Create the new branch from the base branch
                    echo "Creating new branch ${newBranch} from ${baseBranch}"
                    sh """
                        git checkout ${baseBranch}
                        git pull origin ${baseBranch}
                        git checkout -b ${newBranch}
                    """
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
        stage('Publish Branch') {
            when {
                expression {
                    return currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                script {
                    def newBranch = 'new-branch'
                    
                    // Push the new branch to the remote repository
                    echo "Pushing new branch ${newBranch} to origin"
                    sh """
                        git push origin ${newBranch}
                    """
                }
            }
        }
    }
}