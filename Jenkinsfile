pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'test -f index.html'
            }
        }

        stage('Test') {
            steps {
                sh "grep -qi '<html' index.html"
            }
        }
         stage('Docker Build') {
            steps {
                sh 'docker build -t jenkin-demo:latest .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                    docker rm -f jenkin-demo || true
                    docker run -d \
                      --name jenkin-demo \
                      -p 8081:80 \
                      jenkin-demo:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl -fsS http://127.0.0.1:8081/'
            }
        }
        
    }
}
