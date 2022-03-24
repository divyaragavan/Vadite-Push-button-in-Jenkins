#!groovy

testParams = [:]


pipeline {
  agent aa{
        def deployOptions = 'no\nyes'
        def userInput = input(
          id: 'userInput', message: 'Are you prepared to deploy?', parameters: [
          [$class: 'ChoiceParameterDefinition', choices: deployOptions, description: 'Approve/Disallow deployment', name: 'deploy-check']
          ]
        )
        echo "you selected: ${userInput}"
    }
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
    booleanParam(name: 'RUN_STAGE1',
                 defaultValue: true,
                 choices: ['testbed1', 'tesetbed2', 'tesetbed3', 'tesetbed4'],
				 description: 'Run the STAGE1')	                 	                   
    booleanParam(name: 'RUN_STAGE2',
                 defaultValue: false,
                 description: 'RUN_STAGE2')
    booleanParam(name: 'RUN_STAGE3',
                 defaultValue: false,
                 description: 'Run STAGE3')
  }


  stages {
        stage('stage1') {
          when {
            expression { params.RUN_STAGE1 == true }
          }
          input {
                message "Select Test Bed you want to choose"
                ok "Select"
                parameters {
                    choice(name: 'OR-PODS', choices: ['testbed1', 'tesetbed2', 'tesetbed3', 'tesetbed4'])
                }}
          steps {
            script {
              echo "Hi STAGE-1"              
            }
          }
        }
      }
}
