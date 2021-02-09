
pipeline {
    agent any
    environment{
        MY_FILE = fileExists '/usr/local/kafka.postman_collection1.json'
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
       
        stage('conditional if exists')
            when { expression { MY_FILE == 'true' } }
            steps {
               input message: "Shall we build more?"  
               echo "file exists kafka.postman_collection1.json"
            }
        }
         stage('deploy test'){
             steps {
                  sh 'cp kafka.postman_collection.json /usr/local'
                  sh 'newman run /usr/local/kafka.postman_collection.json -k --ssl-client-cert /opt/kafka/security/kafkarestc_client.cer --ssl-client-key /opt/kafka/security/kafkarestc_client-key.pem'       
                  }
                }
           }
    post {
        always {
            echo 'Test run completed'
            cucumber buildStatus: 'UNSTABLE', failedFeaturesNumber: 999, failedScenariosNumber: 999, failedStepsNumber: 3, fileIncludePattern: '**/*.json', skippedStepsNumber: 999
        }
        success {
            echo 'Successfully!'
        }
        failure {
            echo 'Failed!'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
    }
}
