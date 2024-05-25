pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'LMS Code Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_TOKEN="sqp_c7c211999230b21caaa3b0a53d20fa5dda305cda"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=kms'
            }
        }

        stage('Build LMS') {
            steps {
                echo 'LMS Build'
                sh 'cd webapp && npm install && npm run build'
            }
        }

        stage('Release LMS') {
            steps {
                script {
                    echo "Publish LMS Artifacts"       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:kings --upload-file webapp/dist-${packageJSONVersion}.zip http://65.0.11.240:8081/repository/jms-application/"     
                }
            }
        }

        stage('Deploy LMS') {
            steps {
                script {
                    echo "Deploy LMS"       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version  
                    sh "curl -u admin:kings -X GET 'http://65.0.11.240:8081/repository/jms-application/dist-${packageJSONVersion}.zip' --output dist-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -f /var/www/html/*'
                    sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
                }
            }
        }
    }
}
