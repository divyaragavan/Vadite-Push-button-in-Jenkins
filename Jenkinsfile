#!groovy

testParams = [:]

pipeline {
  agent none
  parameters {
    booleanParam(name: 'RELEASE_PACKAGE',
                 defaultValue: true,
                 description: 'Enables publishing to artifactory when enabled')
    booleanParam(name: 'FAST_PUBLISH',
                 defaultValue: env.BRANCH_NAME == "master",
                 description: 'Skips analysis and testing when asserted')
    separator(name: "CI_PIPELINE", sectionHeader: "CI Pipeline: Regularly executed test stages")
    //Ordered alphabetically - OLT specific at top
    booleanParam(name: 'RUN_STAGE1',
                 defaultValue: false,
                 description: 'Run the STAGE1')
    separator(name: "MCP_Upgrade", sectionHeader: "Downstream Jobs - MCP Upgrade")
    booleanParam(name: 'RUN_MCP_UPGRADE',
                 defaultValue: false,
                 description: 'Run the MCP upgrade test stage')
    separator(name: "LAST_AUTOMATION", sectionHeader: "Downstream Jobs - Team LAST Automation - Stages and Parameters")
    //Ordered alphabetically - OLT specific at top
    booleanParam(name: 'RUN_SDX6010_REGRESSION',
                 defaultValue: false,
                 description: 'Run regression on SDX 6010')
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
    stage('Analysis - CI Pipeline Stages') {
      agent { label 'common_builder' }
      when {
        beforeAgent true
        not { expression { SKIP_PIPELINE } }
        not { expression { params.FAST_PUBLISH } }
      }
      steps {
        sshagent(['github.adtran.com-SSH']) {
          withCredentials([string(credentialsId: 'github-api-token', variable: 'GITHUB_TOKEN')]) {
            sh 'make build-all'
          }
        }
        dir('analysis') {
          sh 'tar -zxvf ../$(make -sC .. bundle-filename)'
          script {
          echo "Inside script"           
            }
          }
        }
      }
    }
    stage('CI Pipeline Tests') {
      when {
        beforeAgent true
        not { expression { SKIP_PIPELINE } }
        not { expression { params.FAST_PUBLISH } }
      }
      parallel {
        //CI pipeline: Regularly executed test suites (alphabetical - OLT specific at top)       
        stage('Test Leaf Spine Onboarding') {
          when {
            expression { params.RUN_LEAF_SPINE_ONBOARDING == true }
          }
          environment {
            OS_PROJECT_NAME = "${testParams['APPLICATION']['leaf-spine-onboarding']['OS_PROJECT_NAME']}"
            OS_PROJECT_ID = "${testParams['APPLICATION']['leaf-spine-onboarding']['OS_PROJECT_ID']}"
          }
          steps {
            script {
              runTestLeafSpineOnboarding('leaf-spine-onboarding')
            }
          }
        }
        }
    }
  }
}
