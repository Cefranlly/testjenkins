pipeline {
  agent any
  parameters {
        string(name: 'AWS_DEFAULT_REGION', defaultValue: 'us-east-1', description: 'The region to deploy to'),
        choice(
            choices: 'first_deploy\nother_deploy'
            description: 'during the first deploy AWS services must be created',
            name: 'DEPLOY_TYPE'
        )
  }
  stages {

    stage('Checkout Git') {
      steps {
      git poll: true, url: 'git@github.com:FOXITES/ba-dbi-connectors.git'
      }
    }

    stage('Zip and push files') {
      steps {
      sh "aws cloudformation deploy --template-file "devops\cloudformation.yaml" --stack-name "paidsocialmedia""
      }
    }
  }
}