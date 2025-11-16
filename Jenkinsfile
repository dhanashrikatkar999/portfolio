pipeline {
  agent any

  environment {
    GITHUB_CRED_ID = 'Jenkins1'   // Jenkins credential id holding Personal Access Token
    REPO = 'https://github.com/dhanashrikatkar999/portfolio'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'No build needed for HTML/CSS project.'
      }
    }

    stage('Publish to gh-pages') {
      steps {
        withCredentials([string(credentialsId: env.GITHUB_CRED_ID, variable: 'GHTOKEN')]) {
          sh '''
            git config user.name "jenkins"
            git config user.email "jenkins@localhost"
            git remote set-url origin https://$GHTOKEN@github.com/${REPO}.git

            rm -rf .git
            git init
            git checkout -b gh-pages

            git add .
            git commit -m "Deployed by Jenkins build ${BUILD_NUMBER}" || true
            git push -f origin gh-pages
          '''
        }
      }
    }
  }
}
