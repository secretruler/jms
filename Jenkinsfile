pipeline {
    agent any
    stages {
 
        stage('Deploying LMS application') {
            steps {
                echo "Deploying started"
                script {
                    echo "Deploying  lms applications"
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    sh "curl -u admin:lms12345 -X GET \'http://65.0.11.240:8081/repository/jms-application/lms-1.2.zip\' --output lms-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -f /var/www/html/*'
                    sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
                }
            }
        }

      
    }
}
