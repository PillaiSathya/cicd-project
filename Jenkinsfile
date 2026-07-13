pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {


        stage('Build') {
            steps {
                sh 'mvn clean package'
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
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.projectKey=cicd-project \
                    -Dsonar.host.url=http://host.docker.internal:9000 \
                    -Dsonar.login=$SONAR_TOKEN
                    """
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

        stage('Upload to Nexus') {
            steps {
                sh """
                mvn deploy \
                -DskipTests \
                -DaltDeploymentRepository=nexus::default::http://host.docker.internal:8081/repository/maven-releases/
                """
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-project:latest .'
            }
        }

