pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VikramAagiri/node-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t node-docker-app:${BUILD_NUMBER} .
                docker tag node-docker-app:${BUILD_NUMBER} vikramaagiri/node-docker-app:${BUILD_NUMBER}
                '''
            }
        }

       /* stage('Push Docker Image') {
            steps {
                sh 'docker push vikramaagiri/node-docker-app:${BUILD_NUMBER}'
            }
        } */
        
        stage('Create container') {
    steps {
        sh '''
        docker stop node-app || true
        docker rm node-app || true
        docker run -d -p 3000:8080 --name node-app vikramaagiri/node-docker-app:${BUILD_NUMBER}
        '''
    }
}
    



    }
}
