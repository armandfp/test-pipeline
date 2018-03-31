pipeline {
    agent any
    stages {
        stage('test login') {
            steps {
                echo 'test login'
            }
        }
        stage('test build') {
            steps {
                echo 'test build'
                sh 'sleep 3'
            }
        }
        stage('test stage deploy') {
            steps {
                echo 'doing deploy'
                echo 'extra step!'
                sh 'sleep 1'
            }
        }
        stage('test deploy prod') {
            input {
                message ">> Please select one option:"
                ok "Go prod?"
            }
            steps {
                echo 'doing prod deploy'
            }
        }
    }
}
