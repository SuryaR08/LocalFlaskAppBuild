pipeline {
    agent { label 'docker-agent' }
    stages {
        stage('Clone Repository') {
            steps {
                sh 'rm -rf LocalFlaskAppBuild || true'
                sh 'git clone https://github.com/SuryaR08/LocalFlaskAppBuild.git'
                echo "Repository cloned successfully."
            }
        }
        stage('Run') {
            steps {
                dir('LocalFlaskAppBuild')
                {
                sh 'python3 app.py > flask.log 2>&1 &'
                sh 'tail -f flask.log'
                }
            }
        }
    }
}