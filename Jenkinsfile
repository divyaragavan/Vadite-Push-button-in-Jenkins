#!groovy

testParams = [:]


pipeline {
  agent none  
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
    booleanParam(name: 'STAGE1',
                 defaultValue: true,
				 description: 'Run the STAGE1')	 
    choice(name: 'OR_PODS', choices: ['testbed1', 'tesetbed2', 'tesetbed3', 'tesetbed4'])                 
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
            expression { params.STAGE1 == true }
          }
          steps {
            script {
                if (params.OR_PODS.contains('testbed1')) 
                {
                 echo "TESTBED1"
                }
                else if (params.OR_PODS.contains('testbed2')) 
                {
                 echo "TESTBED2"
                }
                else if (params.OR_PODS.contains('testbed3')) 
                {
                 echo "TESTBED3"
                }                
                else if (params.OR_PODS.contains('testbed4')) 
                {
                 echo "TESTBED4"
                }                                
            }
          }
        }
      }
}
