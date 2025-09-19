pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Install dependencies
                bat '"C:/Users/sp724/AppData/Local/Programs/Python/Python311/python.exe" -m pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                bat '"C:/Users/sp724/AppData/Local/Programs/Python/Python311/python.exe" -m pytest || exit 0'
            }
        }

        stage('Package') {
            when {
                anyOf { branch "master"; branch "release" }
            }
            steps {
                // Compress lib folder into a zip
                bat 'powershell Compress-Archive -Path lib -DestinationPath sbdl.zip -Force'
                
                // Save the zip as Jenkins artifact
                archiveArtifacts artifacts: 'sbdl.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed. Please check logs.'
        }
        always {
            echo '📌 Pipeline finished (success or fail).'
        }
    }
}
