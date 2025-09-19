pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip.exe" install -r requirements.txt'

            }
        }
        stage('Test') {
            steps {
                 bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pytest.exe"'
            }
        }
        stage('Package') {
            when {
                anyOf { branch "master"; branch "release" }
            }
            steps {
                bat 'powershell Compress-Archive -Path lib -DestinationPath sbdl.zip -Force'
            }
        }
    }
}
