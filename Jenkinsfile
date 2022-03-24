#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')                 
    choice(name: 'ORPODS', choices: ['testbed1', 'tesetbed2'], description: 'Choose testbed')                     
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

  stages {
        stage('stage1') {
          when {
            expression { params.RUN_STAGE1 == true }
          }
          input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }}
          steps {
            script {
              echo "Hi STAGE-1"              
            }
          }
        }
      }
}
