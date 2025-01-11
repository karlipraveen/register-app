pipeline{
    agent { any }
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
    }
}