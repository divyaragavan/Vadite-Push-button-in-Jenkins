#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
	activeChoiceParam('STAGE_ONBOARDING') {
		description('Select testbed you wan to run')
        filterable()
		choiceType('SINGLE_SELECT')
		groovyScript {
			script('''return ['web-service', 'proxy-service', 'backend-service']''')
			fallbackScript('"fallback choice"')
		}}              
    choice(name: 'ORPODS', choices: ['testbed1', 'tesetbed2'], description: 'Choose testbed')                 
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
        stage('stage1') {
          when {
            expression { params.STAGE_ONBOARDING == true }
          }
          steps {
            script {
              echo "Hi STAGE-1"
            }
          }
        }
      }
}
