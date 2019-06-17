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
                sh "curl https://api.bitbucket.org/2.0/repositories/dustin-beckett/testing-jenkins-bump/pullrequests \\\n" +
                        "    -u dustin.beckett@genesys.com:Hunter\\!2324 \\\n" +
                        "    --request POST \\\n" +
                        "    --header 'Content-Type: application/json' \\\n" +
                        "    --data '{\n" +
                        "        \"title\": \"Jenkins automatic version bump\",\n" +
                        "        \"source\": {\n" +
                        "            \"branch\": {\n" +
                        "                \"name\": \"master\"\n" +
                        "            }\n" +
                        "        }\n" +
                        "    }'"
            }
        }
    }
}