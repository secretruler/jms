pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo "Analysing the code"
                sh 'cd webapp'
                sh 'sudo docker run --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_LOGIN="sqp_741f1e1ce288d818158f5f4b1358793658fedfb8" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=ems'
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