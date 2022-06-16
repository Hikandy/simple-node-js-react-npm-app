pipeline {
    agent {
        docker {
            image 'node'
            args '-p 3000:3000'
            label 'cent'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('test') {
            steps {
                sh 'npm install --same-dev cross-env'
                sh 'npm test'
            }
        }
        stage('Deliver') {
            steps {
                sh 'npm run build'
                sh 'npm start &'
                sh 'sleep 2'
                sh 'echo $1 > .pidfile'
                input 'click to stop'
                sh 'kill $(cat .pidfile)'

            }
        }
    }
}
