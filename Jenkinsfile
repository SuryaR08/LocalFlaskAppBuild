pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SuryaR08/LocalFlaskAppBuild.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Stop Previous Flask App') {
            steps {
                script {
                    sh '''
                    PID=$(lsof -ti:5000)  # Find process running on port 5000
                    if [ ! -z "$PID" ]; then
                        echo "Stopping existing Flask app with PID $PID"
                        kill -9 $PID
                    fi
                    '''
                }
            }
        }

        stage('Run Flask App') {
            steps {
                script {
                    sh 'nohup python3 app.py &'
                }
            }
        }
    }

    post {
        always {
            emailext (
                to: 'suryaraja8903@gmail.com',
                subject: "Jenkins Build Status: ${currentBuild.currentResult}",
                body: """Build Summary:
                - Job Name: ${env.JOB_NAME}
                - Build Number: ${env.BUILD_NUMBER}
                - Build Status: ${currentBuild.currentResult}
                - Build URL: ${env.BUILD_URL}
                """,
                mimeType: 'text/plain'
            )
        }
    }
}
