pipeline {
    // Clean workspace before doing anything
  
	agent any
    try {
	stages {
        stage ('Clone') {
            checkout scm
            
        }
        stage ('Build') {
            bat "cd SQLSource \n ExecScripts.bat"
        }
       stage ('Tests') {
         parallel   
            'unit': {
                bat "java -jar target\\tafd.jar"
            },
            'integration': {
                bat "echo 'shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            //update dashboard
            bat "echo 'shell scripts to deploy to server...'"
        }
	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
