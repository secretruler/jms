pipeline {
    agent any
    stages {
        stage('Sonar Analysis') {
            steps {
                echo "Analysing the code"
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://65.0.11.240:9000" -e SONAR_TOKEN="sqp_39a60b31af7b26c8b18e9d895fbaccfad8f4b9fd" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=kin'
            }
        }
        stage('Building LMS') {
            steps {
                echo "test Analysis started"
                sh 'cd webapp && npm install && npm run build'
                echo "test Analysis completed"
            }
        }
        stage('Releasing LMS application') {
            steps {
                echo "Releasing started"
                script {
                    echo "publishing the lms applcations"
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:kings --upload-file webapp/dist-${packageJSONVersion}.zip http://65.0.11.240:8081/repository/jms-application/"
                    echo  "releasing completed"
                }
            }
        }

        stage('Deploying LMS') {
            steps {
                echo "Deploying started"
                script {
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    sh "curl -u admin:kings -X GET 'http://65.0.11.240:8081/repository/jms-application/lms-1.1.zip' --output lms-1.1.zip"
                    sh "sudo rm -f /var/www/html/*"
                    sh "sudo unzip  -o dist-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"

                }
                
            }
        }


    }
}