node {
    // Clean workspace before doing anything
  

    try {
        stage ('Clone') {
            checkout scm
            
        }
        stage ('Build') {
           
        }
       stage ('Tests') {
            parallel 'static': {
                bat "echo 'shell scripts to run static tests...'"
            },
            'unit': {
                bat "\"C:\Program Files\Java\jre1.8.0_91\bin\java\" -jar target\tafd.jar"
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
