pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo "Analysing the code"
                sh 'cd webapp'
                sh 'sudo docker run  --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_LOGIN="sqp_6b8b1bd71230ce7e06220ca1b30c2ed28c7ea2b8"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=jms'
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