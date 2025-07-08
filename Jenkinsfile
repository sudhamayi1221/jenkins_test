pipeline {
    agent any

    environment {
        // Optional: Define environment variables
        VERSION = "${env.GIT_TAG_NAME}"
    }

    stages {
        stage('Check for Tag') {
            when {
                expression {
                    // Proceed only if this is a tag build
                    return env.GIT_BRANCH =~ /^refs\/tags\/.*/
                }
            }
            steps {
                echo "Triggered by tag: ${env.GIT_BRANCH}"
                script {
                    // Extract tag name from ref
                    env.GIT_TAG_NAME = env.GIT_BRANCH.replaceFirst(/^refs\/tags\//, "")
                    echo "Releasing version: ${env.GIT_TAG_NAME}"
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building release ${env.GIT_TAG_NAME}"
                // e.g., sh 'npm install && npm run build'
            }
        }

        stage('Deploy or Publish') {
            steps {
                echo "Deploying version ${env.GIT_TAG_NAME}"
                // e.g., sh './deploy.sh'
            }
        }
    }
}

