#!groovy

testParams = [:]


pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')                                         
    booleanParam(name: 'RUN_STAGE1',
                 defaultValue: true,
		 description: 'Run the STAGE1')	                   
    booleanParam(name: 'RUN_STAGE2',
                 defaultValue: false,
                 description: 'RUN_STAGE2')
    booleanParam(name: 'RUN_STAGE3',
                 defaultValue: false,
                 description: 'Run STAGE3')
  }

if (params.RUN_STAGE1 == true) {
  parameters[choice(name: 'OR-PODS', choices: ['testbed1', 'tesetbed2', 'tesetbed3', 'tesetbed4'])]
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
