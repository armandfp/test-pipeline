node {
    stage ('Checkout') {
        checkout scm
    }
    notifyBuild('STARTED')
    stage('test login') {
        echo 'connect to server'
        echo 'test login'
    }
    stage('test build') {
        echo 'test build'
        echo 'extra test build'
        sh 'sleep 3'
    }
    stage('test stage deploy') {
        echo 'doing deploy'
        echo 'extra step!'
        sh 'sleep 1'
    }
    notifyBuild('WAITING')
    stage('test deploy prod') {
        input (message: ">> Please select one option:", ok: "Go prod?")
        echo 'doing prod deploy'
    }
    notifyBuild(currentBuild.result)
}

def notifyBuild(String buildStatus = 'STARTED') {
    buildStatus =  buildStatus ?: 'SUCCESS'
    def summary = ""
    def info = "${env.JOB_NAME}:${env.BRANCH_NAME} [${env.BUILD_NUMBER}]"
    color = 'BLUE'
    colorCode = '#439FE0'

    if (buildStatus == 'STARTED') {
        summary =  "Build started: ${info}"
    } else if (buildStatus == 'SUCCESS') {
        color = 'GREEN'
        colorCode = '#49bc29'
        summary =  "Build success: ${info}"
    } else if (buildStatus == 'WAITING') {
        color = 'BLUE'
        colorCode = '#439FE0'
        summary =  "Build awaiting approval: ${info}"
    } else {
        color = 'RED'
        colorCode = '#FF0000'
        summary =  "Build failed: ${info}"
    }

    // Send notifications
    //if(env.BRANCH == "master") {
        slackSend (color: colorCode, message: summary)
    //}
}