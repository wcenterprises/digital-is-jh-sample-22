library identifier: "[PROJECT-OWNER]-jenkins-shared-pipelines@v1", changelog: false
library identifier: "environments@master", changelog: false

properties(
[
    buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '30', numToKeepStr: '10')),
])
    
if (env.BRANCH_NAME == "main") {

    def version = null
    def appName = null 
                      
    node {
        checkout scm
        sh("git checkout $env.BRANCH_NAME")
        //Make sure we are up to date.
        sh("git pull origin $env.BRANCH_NAME")
        sh("git pull --tags")
        version = sh(script: "git describe --abbrev=0 --tags", returnStdout: true).trim()
        // hard coding for now
        appName = "{{ REPO-NAME }}"
    }
    [PROJECT-OWNER]EnvironmentsApplicationDeploy(
        appNames: [appName],
        slackChannel: "{{ SLACK-CHANNEL }}",
        slackTeamName: "{{ SLACK-TEAM }}",
        releaseVersion: version,
        namespace: "digital-is"
    )
}
