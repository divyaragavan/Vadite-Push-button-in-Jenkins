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
				 description: 'Run the STAGE1'
				 parameters{
				     choice(name: 'OR-Testbeds',
	                 choices: ['or-large-1', 'or-small', 'or-medium', 'or-x-large']
                     description: 'these are choices')
				 })				
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
        beforeAgent true
        changeRequest()
        expression { isIndexingRebuild() }
      }
      steps {
        script {
          currentBuild.result = currentBuild.previousBuild.result
          SKIP_PIPELINE = true
        }
      }
    }
      }
}

