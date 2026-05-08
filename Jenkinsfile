pipeline {
    agent any

    tools {
        maven 'mvn'
        jdk 'jdk17'
    }

    stages {

        stage('First Stage') {
            steps {
                sh 'date'
                sh 'pwd'
                sh 'ls'
            }
        }

        stage('Check Versions') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
        stage('app port'){
            steps{
                 sh 'echo "server.port=9090" >> src/main/resources/application.properties'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Run') {
            steps {
                sh 'nohup java -jar target/*.jar --server.port=9090 > app.log 2>&1 &'
                sleep 300
            }
        }

    }
}
