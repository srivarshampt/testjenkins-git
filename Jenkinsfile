
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
                if (fileExists('kafka.postman_collection')) {
                 echo 'Yes'
                } else {
                  echo 'No'
}
            }
        }
    }
}
