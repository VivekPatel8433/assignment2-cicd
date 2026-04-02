pipeline {
    agent any

    tools {
        nodejs 'NodeJS-22' 
    }

    environment {
        NETLIFY_SITE_ID = 'your-site-id-here'
        NETLIFY_TOKEN = credentials('netlify-token')
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Deploy') {
            steps {
                sh 'npx netlify-cli deploy --prod --dir=build --site=$NETLIFY_SITE_ID --auth=$NETLIFY_TOKEN'
            }
        }
    }
}