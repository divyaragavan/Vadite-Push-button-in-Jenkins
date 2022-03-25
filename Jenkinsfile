#!groovy

testParams = [:]

properties([parameters([[$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT', filterLength: 1, filterable: false, name: 'CHOICES', randomName: 'choice-parameter-89419589178408', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return[\'error\']'], script: [classpath: [], sandbox: false, script: '''return[
\'aaa\',
\'bbb\',
\'ccc\'
]''']]]])])

pipeline {
  agent none  
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
    booleanParam(name: 'RUN_STAGE1',
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
            expression { params.OR_PODS == true }
          }
          steps {
            script {
              echo "Hi STAGE-1"              
            }
          }
        }
      }
}
