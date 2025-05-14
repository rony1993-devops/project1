pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/rony1993-devops/project1.git', branch: 'master'
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t rony1993/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push rony1993/staragileprojectfinance:v1'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -itd --name My-first-container -p 8083:8081 rony1993/staragileprojectfinance:v1'
            }
        }
    }
}
