pipeline {
  agent none
  parameters {
        choice(
            choices: ['dev' , 'test','uat','all'],
            description: '',
            name: 'REQUESTED_ACTION')
    }

  stages {
    stage("dev") {
      agent any
      when {
                expression { params.REQUESTED_ACTION == 'dev' || params.REQUESTED_ACTION == 'all' }
            }
      steps {
        echo "Building dev environment"
      }
    }
    stage("test") {
      agent none
      checkpoint
      when {
                expression { params.REQUESTED_ACTION == 'test' || params.REQUESTED_ACTION == 'all' }
            }
      steps {
        timeout(time: 60, unit: 'SECONDS') {
            input message: 'Do you want to proceed?', ok: 'Yes'
        }
		echo 'running test phase'
      }
    }
    stage("uat") {
      agent any
      checkpoint
      when {
                expression { params.REQUESTED_ACTION == 'uat'  || params.REQUESTED_ACTION == 'all' }
      }
      steps {
        echo 'running uat phase'
      }
    }
  }
}
