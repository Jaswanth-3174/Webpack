pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build with Webpack') {
            steps {
                bat 'npx webpack --mode production'
            }
        }

        stage('Prepare GitHub Pages Folder') {
            steps {
                // Delete old docs folder and recreate it
                bat 'if exist docs rmdir /S /Q docs'
                bat 'mkdir docs'
                // Copy contents of dist to docs
                bat 'xcopy /E /Y dist\\* docs\\'
            }
        }

        stage('Push to GitHub') {
            steps {
                bat '''
                git config user.name "Jenkins"
                git config user.email "jenkins@example.com"
                git add docs
                git commit -m "Deploy Webpack build to GitHub Pages"
                git push origin main
                '''
            }
        }
    }
}
