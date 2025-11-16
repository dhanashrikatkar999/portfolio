pipeline {
    agent any

    environment {
        GITHUB_CRED_ID = 'github-pat'  
        REPO = 'dhanashrikatkar999/portfolio'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'No build needed for static site.'
            }
        }

        stage('Publish to gh-pages') {
    steps {
        withCredentials([string(credentialsId: env.GITHUB_CRED_ID, variable: 'GHTOKEN')]) {
            powershell """
                git config user.name 'jenkins'
                git config user.email 'jenkins@localhost'

                if (Test-Path .git) { Remove-Item -Recurse -Force .git }

                git init
                git checkout -b gh-pages
                git add .
                git commit -m "Deployed by Jenkins build $env:BUILD_NUMBER"

                git remote add origin "https://$env:GHTOKEN@github.com/$env:REPO.git"

                git push -f origin gh-pages
            """
        }
    }
}

    }
}
