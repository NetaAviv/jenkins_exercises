pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            steps {
                script {
                    // Check if requirements.txt exists before installing dependencies
                    if (fileExists('requirements.txt')) {
                        sh 'pip install -r requirements.txt'
                    } else {
                        echo 'No requirements.txt found. Skipping dependency installation.'
                    }
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'python -m unittest discover tests'
            }
        }
        
        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying application...'
                // Add deployment commands here if needed
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
    }
}
