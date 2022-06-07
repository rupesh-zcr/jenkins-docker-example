pipeline{
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'dockerhubpwd', url: 'https://github.com/rupesh-zcr/jenkins-docker-example.git']]])

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t ankush8421/my-app-1.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'Dockerhubpwd', variable: 'Password')]) {
                    sh 'docker login -u ankush8421 -p ${Password}'
                 }  
                 sh 'docker push ankush8421/my-app-1.0'
                }
            }
        }
    }
}
