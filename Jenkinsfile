#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
    booleanParam(name: 'STAGE_ONBOARDING',
                 defaultValue: true,
                 description: 'THIS IS STAGE_ONBOARDING')                     
    booleanParam(name: 'RUN_STAGE1',
                 defaultValue: false,
				 description: 'Run the STAGE1')				
    booleanParam(name: 'RUN_STAGE2',
                 defaultValue: false,
                 description: 'RUN_STAGE2')
    booleanParam(name: 'RUN_STAGE3',
                 defaultValue: false,
                 description: 'Run STAGE3')
  }

  stages {
        stage('STAGE_ONBOARDING') {
          when {
            expression { params.STAGE_ONBOARDING == true }
          }
          steps {
            parameters(choice(name: 'OR_PODS', choices: ['testbed1', 'tesetbed2'], description: 'Choose testbed'))
          }
        }
      }
}
