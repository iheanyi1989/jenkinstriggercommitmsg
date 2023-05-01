pipeline {
    agent any // Run the pipeline on any available agent

    environment {
        GIT_COMMIT_MSG = "" // Initialize an environment variable to store the commit message
    }

    options {
        skipDefaultCheckout() // Skip the default checkout step, allowing us to control the checkout process
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    def scmVars = checkout scm // Manually checkout the code from the source code repository
                    // Retrieve the latest commit message using git log and store it in the GIT_COMMIT_MSG environment variable
                    GIT_COMMIT_MSG = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
                }
            }
        }

        stage('Check Commit Message') {
            steps {
                script {
                    // Compare the retrieved commit message with the desired string 'TEST-123'
                    if (GIT_COMMIT_MSG == 'TEST-123') {
                        echo "Commit message is 'TEST-123', proceeding with the pipeline"
                    } else {
                        // If the commit message does not match 'TEST-123', abort the pipeline
                        currentBuild.result = 'ABORTED'
                        error "Commit message is not 'TEST-123', aborting the pipeline"
                    }
                }
            }
        }

        stage('Your Job') {
            steps {
                echo 'Executing the main job'
                echo 'Test Success' // Indicate that the test was successful
                // Place any additional steps for your job here
            }
        }
    }
}
