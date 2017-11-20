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
            parallel
            'unit': {
                //call taf , add atleast 10 tables
             bat   "C:\Program Files\Java\jre1.8.0_91\bin\java" -jar target\tafd.jar;
                bat "echo 'shell scripts to run unit tests...'"
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
