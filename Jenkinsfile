#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'THIS IS RELEASE PACKAGE')
    separator(name: "CI_PIPELINE", sectionHeader: "CI Pipeline: Regularly executed test stages")
    //Ordered alphabetically - OLT specific at top
    booleanParam(name: 'RUN_STAGE1',
                 defaultValue: false,
                 description: 'Run the STAGE1')
    separator(name: "MCP_Upgrade", sectionHeader: "Downstream Jobs - MCP Upgrade")
    booleanParam(name: 'RUN_STAGE2',
                 defaultValue: false,
                 description: 'RUN_STAGE2')
    separator(name: "LAST_AUTOMATION", sectionHeader: "Downstream Jobs - Team LAST Automation - Stages and Parameters")
    //Ordered alphabetically - OLT specific at top
    booleanParam(name: 'RUN_STAGE3',
                 defaultValue: false,
                 description: 'Run STAGE3')
  }

  options {
    buildDiscarder(logRotator(numToKeepStr: '30'))
    timestamps()
  }

  stages {
    stage('Skip Pipeline for Indexing Rebuild') {
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
