pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo "Analysing the code"
                sh 'cd webapp'
                sh 'sudo docker run --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_LOGIN="sqp_9a1a9cc1b22654a850b0fc33bbe45c746524f93a" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=jms'
            }
        }
        stage('Test') {
            steps {
                echo "test completed"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy completed"
            }
        }
    }
}