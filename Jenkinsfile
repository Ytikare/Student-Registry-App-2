node{
    agent any

    stages{
        stage('Npm build'){
            steps {
                bat 'npm install'
            }
        }
        stage('Fix repo vulnerabilities') {
            steps {
                def adutitResults = bat(script: 'npm audit --json', returnStdout: true).trim();
                if (adutitResults.contains('moderate') | adutitResults.contains('high') | adutitResults.contains('low')){
                    echo "Vulnerabilities found. Fixing..."
                    bat 'npm audit fix'
                }
                else{
                    echo "No vulnerabilities found."
                }
            }
        }
        stage('Run tests'){
            steps {
                bat 'npm run test'
            }
        }
        stage('Deployment'){
            echo "Deploying..."
        }
    }
}