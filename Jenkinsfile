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
    choice(name: 'OR-PODS', choices: ['testbed1', 'tesetbed2', 'tesetbed3', 'tesetbed4'])                 
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
            expression { params.OR-PODS == true }
          }
          steps {
            script {
              echo "Hi STAGE-1"              
            }
          }
        }
      }
}
