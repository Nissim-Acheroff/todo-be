pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline-be -t image-builder --target builder .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f docker-pipeline-be -t nissimacheroff/todo-be:jenkins-$BUILD_NUMBER --target delivery .'
            }
        }
        stage('push') {
            environment {
                dockerpwd = credentials('docker_pwd')
            }
            steps {
                    sh 'docker login -u nissimacheroff -p ${dockerpwd}'
                    sh "docker push nissimacheroff/todo-be:jenkins-$BUILD_NUMBER"
        }
    }
}
}
