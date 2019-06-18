pipeline {
    agent any
    stages {
        stage('build') {
            steps {

                node('version-bump'){
                    def v = 10;
                }

                sh 'pwd'
                sh 'ls -a'
                sh 'git status'
                sh 'git checkout -b test-branch'
                sh 'mvn build-helper:parse-version versions:set -DnewVersion=\\${parsedVersion.majorVersion}.\\${parsedVersion.minorVersion}.\\${parsedVersion.nextIncrementalVersion}'
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
                        "                \"name\": \"jenkins-automatic-version-bump\"\n" +
                        "            }\n" +
                        "        }\n" +
                        "    }'"
            }
        }
    }
}