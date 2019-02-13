#!groovy

node('master') {
    stage('Checkout') {
        checkout scm
    }
    stage('ShowEnv') {
        sh 'env > env.txt' 
        for (String i : readFile('env.txt').split("\r?\n")) {
              println i
        }
    }
    
    stage('Run tests') {
        try {
        withMaven(maven: 'Maven 3') {
            sh 'mvn clean test -Dwebdriver.type=remote -Dwebdriver.url=http://zalenium:4444/wd/hub -Dwebdriver.cap.browserName=chrome'
        }
       } finally {
            junit testResults: 'target/*.xml', allowEmptyResults: true
            archiveArtifacts 'target/**'
       }
    }
}
