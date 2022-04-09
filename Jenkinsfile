pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/jodada1/Myproject.git'
            }
        }
        stage("SonarQube analysis 1") {
            steps {
                withSonarQubeEnv('mysonar') {
                sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
              }
           } 
        }
        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn package'
            }
        }
        stage('Deploy to Tom') {
            steps {
            deploy adapters: [tomcat9(credentialsId: 'devops',
            path: '',
            url: 'http://3.86.254.63:8080')],
            contextPath: 'default',
            war: '**/*.war'
           }
        }
        
    }
}

