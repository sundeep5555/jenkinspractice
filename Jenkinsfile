pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '''
                echo "Workspace:"
                pwd
                ls -l

                echo "Moving to demoapp"
                cd demoapp

                mvn -version
                mvn clean test
                '''
            }
        }
    }
}
