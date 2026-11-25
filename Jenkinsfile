
pipeline {
    agent none

    environment {
        DOCKERHUB_USERNAME = 'lubina123'
        DOCKERHUB_REPOSITORY = 'companywebsite'
        IMAGE_NAME = 'lubina123/companywebsite'
        CONTAINER_NAME = 'company-website'
        GITHUB_REPOSITORY_URL = 'https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git'
    }

    stages {

        stage('Checkout and Build') {
            agent {
                label 'build-server'
            }

            steps {
                git branch: 'main',
                    url: "${GITHUB_REPOSITORY_URL}"

                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Docker Hub Login and Push') {
            agent {
                label 'build-server'
            }

            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DH_USER',
                    passwordVariable: 'DH_PASS'
                )]) {
                    sh '''
                        echo "$DH_PASS" | docker login \
                        -u "$DH_USER" --password-stdin

                        docker push $IMAGE_NAME:latest
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy Website') {
            agent {
                label 'deploy-server'
            }

            steps {
                sh '''
                    docker pull $IMAGE_NAME:latest

                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true

                    docker run -d \
                    --name $CONTAINER_NAME \
                    --restart unless-stopped \
                    -p 9090:80 \
                    $IMAGE_NAME:latest

                    docker ps
                '''
            }
        }

        stage('Verify Website') {
            agent {
                label 'deploy-server'
            }

            steps {
                sh '''
                    sleep 3
                    curl -f http://localhost:9090
                    echo "Website deployed successfully"
                '''
            }
        }
    }
}
