
pipeline {
    agent any

    tools {
       
        maven 'Maven'
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'master',
                    url: 'https://github.com/cjcnkolhe/sonarproject.git'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

      
stage('SonarQube Code Analysis') {
    steps {
        withCredentials([
            string(credentialsId: 'sonarqube-token',
                   variable: 'SONAR_TOKEN')
        ]) {
            sh '''
                mvn org.sonarsource.scanner.maven:sonar-maven-plugin:5.8.0.7211:sonar \
                  -Dsonar.projectKey=my-project \
                  -Dsonar.projectName=my-project \
                  -Dsonar.host.url=http://16.16.194.221:9000 \
                  -Dsonar.token="$SONAR_TOKEN"
            '''
        }
    }
}

    }
}
