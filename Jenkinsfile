pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
              echo "Build Stage is running"
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t romy2003-builder --target builder .'
            }
        }
        stage('Testing stage') {
            steps {
              echo "Testing Stage is running"
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t romy2003-testing --target testing .'
            }
        }
        stage('Delivery stage') {
            steps {
                echo "Delivery Stage is running" 
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t romy2003/todo-fe:jenkins-$BUILD_NUMBER --target delivery .'
            }
        }
        stage('Cleanup') {
            steps {
                echo "Cleanup-stage is running"
                sh 'docker system prune -f'
            }
        }
        stage('Push to Docker') {
            environment {
                dockerpwd = credentials('AlexDoc')
            }
            steps {
                echo "Push to Docker"
                sh 'docker login -u romy2003 -p ${dockerpwd}'
            }
        }
    }
}
