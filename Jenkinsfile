pipeline {
    agent any
    
    tools {
        nodejs 'nodejs20'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Repo Checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/techpentest/NodejS-JEST-main.git'
            }
        }
        
         stage('NPM Install') {
            steps {
                     sh 'npm install'
            }
        }
        
         stage('NPM Test') {
            steps {
                sh '''
                chmod +x ./node_modules/.bin/jest
                npm run test
                '''
            }
        }
        
        stage('SonarQube Analysis') {
	        steps {
                withSonarQubeEnv('sonarqube') {
                      sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.sources=. \
                              -Dsonar.projectKey=nodejs-project1 \
                              -Dsonar.tests=. -Dsonar.test.inclusions=**/*.test.js \
                              -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
                          '''
                 }
             }
         }
         
         stage('Quality Gateway Check') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: false,
                    credentialsId: 'sonar-token'
                }
            }
        }
    }
}
