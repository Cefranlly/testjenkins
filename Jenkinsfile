pipeline {
  agent any

  enviroment{
    SLACK_CHANNEL         = '#deployment'
    SLACK_CREDENTIAL_ID   = 'slack-demo'
    SLACK_TEAM_DOMAIN     = 'PruebasJenkins'
    SLACK_BASE_URL        = 'https://hooks.slack.com/services/'
  }

  parameters {
        string(name: 'AWS_DEFAULT_REGION', defaultValue: 'us-east-1', description: 'The region to deploy to')
        choice(
            choices: 'first_deploy\nother_deploy'
            description: 'during the first deploy AWS services must be created'
            name: 'DEPLOY_TYPE'
        )
  }

  stages {

    stage('Config Slack Notification'){
        steps{
            slackSend baseUrl: env.SLACK_BASE_URL, channel: env.SLACK_CHANNEL, color: '#D4DB40',
            message: 'Welcome to Jenkins!', teamDomain: env.SLACK_TEAM_DOMAIN,
            tokenCredentialId: env.SLACK_CREDENTIAL_ID
        }
    }

    stage('Checkout Git') {
      steps {
      git poll: true, url: 'https://github.com/Cefranlly/testjenkins.git'
      }
    }

    stage('Zip and push files') {
      steps {
      cmd "aws cloudformation deploy --template-file "devops\cloudformation.yaml" --stack-name "paidsocialmedia""
      }
    }
  }
}
