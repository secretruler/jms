pipeline {
    agent any

    stages {
        stage('CODE QUALITY CHECK') {
            steps {
                echo 'Checking..'
                echo " code quality checking......"
                sh 'sudo docker run --rm -e SONAR_HOST_URL="http://15.207.114.76:9000" -e SONAR_LOGIN="sqp_689cb184daa947bf48a3bb8ec8e79bd150f0ffc2" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=ems'
                echo " testing completed "
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd webapp && npm install &&  npm run build'
                echo 'Building completed'
            }
        }
        stage('Read JSON') {
            steps {
                script {
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo "${packageJSONVersion}"
        
                }
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying.....'
            }
        }
    }
}





