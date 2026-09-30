
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
                sh '''
                    mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                        -Dsonar.projectKey=my-project \
                        -Dsonar.projectName=my-project \
                        -Dsonar.host.url=http://65.2.29.116:9000 \
                        -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }
    }
}
