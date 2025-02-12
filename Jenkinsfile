pipeline {
    agent any

    tools {
        maven 'Maven' // Ensure you have Maven installed in Jenkins (Manage Jenkins > Global Tool Configuration)
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KarthiR98/acc-project.git', credentialsId: 'fd1a7274-1684-4e97-a88d-3d5137dea649'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -Dmaven.repo.local=$WORKSPACE/.m2/repository'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build and test completed successfully!'
        }
        failure {
            echo 'Build or test failed!'
        }
    }
}
