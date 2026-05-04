pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=cicd-project
                    '''
                }
            }
        }

// comment this stage temporarily
//        stage('Quality Gate') {
//          steps {
//                timeout(time: 2, unit: 'MINUTES') {
//                  waitForQualityGate abortPipeline: true
//              }
//          }
 //      }

    }

stage('Quality Gate') {
    steps {
        timeout(time: 2, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}}
