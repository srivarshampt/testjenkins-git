
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
        stage('conditional if exists'){
            when { expression { MY_FILE == 'true' } }
            steps {
                echo "file exists"
            }
        }
    }
}
