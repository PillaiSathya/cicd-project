pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PillaiSathya/cicd-project'
            }
        }

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
    }
}

stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('sonar') {
            sh '''
            mvn clean verify sonar:sonar \
            -Dsonar.projectKey=cicd-project \
            -Dsonar.host.url=http://localhost:9000 \
            -Dsonar.login=YOUR_TOKEN
            '''
        }
    }
}

stage('Quality Gate') {
    steps {
        timeout(time: 2, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
