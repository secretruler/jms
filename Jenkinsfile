pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo "Analysing the code"
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_TOKEN="sqp_39a60b31af7b26c8b18e9d895fbaccfad8f4b9fd" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=kin'
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