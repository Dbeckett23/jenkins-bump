pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'Hello World!'
                echo 'The Jenkins file appears to be working correctly.'
                sh 'mvn build-helper:parse-version versions:set -DnewVersion=\\${parsedVersion.majorVersion}.\\${parsedVersion.minorVersion}.\\${parsedVersion.nextIncrementalVersion}'
                sh 'pwd'
                sh 'ls -a'
                sh 'git add .'
                sh 'git commit -m "bumped parent version number"'
                sh 'git checkout -b jenkins-automatic-version-bump'

            }
        }
    }
}