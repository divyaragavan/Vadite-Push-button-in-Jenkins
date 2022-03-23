#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
	activeChoiceParam('RUN_STAGE01') {
		description('Select testbed you wan to run')
		choiceType('SINGLE_SELECT')
		groovyScript {
			script('''return ['web-service','proxy-service','backend-service']''')
			fallbackScript('"fallback choice"')
		}  
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')  
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
        stage('RUN_STAGE01') {
          when {
            expression { params.RUN_STAGE01 == true }
          }
          steps {
            script {
              echo "Hi STAGE-1"
            }
          }
        }
      }
   }
}
