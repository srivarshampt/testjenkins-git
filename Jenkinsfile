
pipeline {
    agent any
    environment{
        MY_FILE = fileExists '/usr/local/kafka.postman_collection.json'
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        boolean testPassed = false
        stage('conditional if exists'){
            when { expression { MY_FILE == 'true' } }
            steps {
                echo "file exists"
                testPassed = true
            }
        }
         stage('deploy'){
            steps {
                if(testPassed){
                   cp  kafka.postman_collection.json /usr/local
                   newman run /usr/local/kafka.postman_collection.json -k --ssl-client-cert /opt/kafka/security/kafkarestc_client.cer --ssl-client-key /opt/kafka/security/kafkarestc_client-key.pem
 
              }
            }
        }

    }
}
