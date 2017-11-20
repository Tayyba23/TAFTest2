node {
    // Clean workspace before doing anything
  

    try {
        stage ('Clone') {
            checkout scm
            
        }
        stage ('Build') {
            bat "test.bat"
        }
       stage ('Tests') {
            parallel 'static': {
                bat "echo 'shell scripts to run static tests...'"
            },
            'unit': {
                bat "echo 'shell scripts to run unit tests...'"
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
