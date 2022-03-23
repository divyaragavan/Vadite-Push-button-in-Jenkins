#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
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
        stage('RUN_STAGE1') {
          when {
            expression { params.RUN_LEAF_SPINE_ONBOARDING == true }
          }
          steps {
            script {
              echo "Hi STAGE-1"
			  activeChoiceParam('RUN_STAGE01') {
		           description('Select testbed you wan to run')
		           choiceType('SINGLE_SELECT')
		           groovyScript {
			                    script('return ['web-service', 'proxy-service', 'backend-service']')
			                    fallbackScript('"fallback choice"')
		                        }  
		          }
            }
          }
        }
      }
}

