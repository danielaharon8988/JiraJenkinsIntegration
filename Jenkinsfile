pipeline {
  agent any

  environment {
    JIRA_CREDENTIALS_ID = 'jira_credentials' // Jenkins credentials ID for Jira
    JIRA_BASE_URL = 'http://172.18.0.3:8080/' // Jira URL
    JIRA_SITE_NAME = 'jira' // Jira site name
  }

  stages {
    stage('Get Last Merged Branch Name') {
      steps {
        script {
          // Get the last commit message and extract the branch name
          def lastCommitMessage = sh(script: 'git log -1 --pretty=format:%s', returnStdout: true).trim()

          // Define a refined pattern to capture only the issue key (DANIEL-3)
          def mergeBranchPattern = ~/Merge pull request #\d+ from (?:([^/]+)/)?([^/]+)/
          def matcher = lastCommitMessage =~ mergeBranchPattern

          if (matcher.find()) {
            // Directly assign the captured issue key to JIRA_ISSUE_KEY
            env.JIRA_ISSUE_KEY = matcher.group(2).trim() // Group 2 captures the issue key
          } else {
            error("No merge found into 'main'. Unable to determine Jira issue key.")
          }
        }
      }
    }

    stage('Transition Jira Issue to Done') {
      steps {
        script {
          def issueKey = env.JIRA_ISSUE_KEY
          if (issueKey) {
            withEnv(["JIRA_SITE=jira"]) {
              def transitionInput = [
                transition: [id: '31']
              ]

              jiraTransitionIssue idOrKey: issueKey, input: transitionInput
            }
          } else {
            error("Jira issue key is null. Cannot transition to Done.")
          }
        }
      }
    }
  }

  post {
    always {
      echo 'Pipeline completed.'
    }
  }
}
