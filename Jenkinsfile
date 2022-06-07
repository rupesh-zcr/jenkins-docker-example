pipeline{
    agent any
    
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'githubpwd', url: 'https://github.com/rupesh-zcr/jenkins-docker-example']]])

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t ankush8421/my-app-2.0 .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'Dockerhubpwd', variable: 'Password')]) {
                    sh 'docker login -u ankush8421 -p ${Password}'
                 }  
                 sh 'docker push ankush8421/my-app-2.0'
                }
            }
        }
    }
}
