pipeline {
    agent any

    tools {
        nodejs 'NodeJS-22'
    }

    environment {
        NETLIFY_SITE_ID = '6f21f1bc-f328-4e7b-becf-568f02d7a72b'
        NETLIFY_TOKEN = credentials('netlify-token')
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                dir('my-app') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                dir('my-app') {
                    sh 'npm test -- --watchAll=false'
                }
            }
        }

        stage('Deploy') {
            steps {
                dir('my-app') {
                    sh 'npx netlify-cli deploy --prod --dir=build --site=$NETLIFY_SITE_ID --auth=$NETLIFY_TOKEN'
                }
            }
        }
    }
}