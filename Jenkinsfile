pipeline {
    agent any
    tools {
            jdk 'Java17'
            maven 'Maven3'
    }
    environment {
            REPO_URL = ' https://github.com/MINAWI0/GestionBibliotheque.git'
            SONARQUBE_CREDENTIALS_ID = 'sonar'
    }
    stages {
         stage('clean work-space') {
                    steps {
                        cleanWs()
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
        stage('Quality Analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar' , credentialsId: SONARQUBE_CREDENTIALS_ID) {
                                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Déploiement simulé réussi'
            }
        }
    }
    post {
        success {
            emailext to: 'minaouimh@gmail.com',
                subject: 'Build Success',
                body: 'Le build a été complété avec succès.'
        }
        failure {
            emailext to: 'minaouimh@gmail.com',
                subject: 'Build Failed',
                body: 'Le build a échoué.'
        }
    }
}
