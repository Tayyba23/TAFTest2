node {
    // Clean workspace before doing anything
  

    try {
        stage ('Clone') {
            checkout scm
            
        }
        stage ('Build') {
            bat "cd SQLSource \n ExecScripts.bat"
        }
       stage ('Tests') {
            parallel 'static': {
                bat "echo 'shell scripts to run TAF TEST...'"
				   bat "java -jar target\\tafd.jar"
            },
            'unit': {
               
			   },
            'integration': {
                bat "echo 'shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            //update dashboard
            bat "echo 'shell scripts to deploy to server...'"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
