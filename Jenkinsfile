pipeline{
    agent any
    tools {
        jdk 'JAVA17'
        maven "Maven3"
    }

    stages {
        stage ("Cleanup Workspace") {
            steps { cleanWs() }
        }

        stage ("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/karlipraveen/register-app.git'
            }
        }

        stage ("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }

        stage ("Test Application"){
            steps {
                sh "mvn test"
            }
        }
        stage ("SonarQube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'Jenkins-sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }            
        }

        stage("Quality Gate"){
            steps {
                waitForQualityGate abortPipeline: false, credentialsId: 'Jenkins-sonarqube-token'
            }
        }
    }
}