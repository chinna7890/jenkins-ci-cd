pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
 master
                git 'github.com/chinna7890/jenkins-ci-cd.git'
                git 'https://github.com/chinna7890/jenkins-ci-cd.git'
              main
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop azure || true
                docker rm azure || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi amazon || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 6060:8080 --name azure amazon'
            }
        }
    }
}
