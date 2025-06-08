pipeline {
    agent any
    
    tools {
        nodejs 'nodejs18'
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
                sh 'npm run test'
            }
        }
        
        // stage('SonarQube Analysis') {
	       // steps {
        //         withSonarQubeEnv('sonarqube') {
        //               sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.sources=. \
        //                       -Dsonar.tests=. -Dsonar.test.inclusions=**/*.test.js \
        //                       -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
        //                   '''
        //          }
        //      }
        //  }
    }
}
