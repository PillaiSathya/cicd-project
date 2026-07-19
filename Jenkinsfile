pipeline {
    agent any

    environment {
        IMAGE_NAME = "pillaisathya/cicd-project"
        IMAGE_TAG = "${BUILD_NUMBER}"
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

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }
	
	stage('Update Kubernetes Manifest') {
    steps {
        sh '''
        sed -i "s|image: pillaisathya/cicd-project:.*|image: pillaisathya/cicd-project:${IMAGE_TAG}|" k8s/deployment.yaml
        cat k8s/deployment.yaml
        '''
    }
}

	stage('Commit and Push Manifest') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'github-token',
            usernameVariable: 'GIT_USER',
            passwordVariable: 'GIT_TOKEN'
        )]) {
            sh '''
            git config user.email "jenkins@local"
            git config user.name "Jenkins"

            git add k8s/deployment.yaml
            git commit -m "ci: update image tag to ${IMAGE_TAG}" || true

            git push https://${GIT_USER}:${GIT_TOKEN}@github.com/PillaiSathya/cicd-project.git HEAD:k8s-argocd-upgrade
            '''
        }
    }
}

    }
}
