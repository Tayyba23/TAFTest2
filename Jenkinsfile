node {
    // Clean workspace before doing anything
    try {
        stage ('Build') {
	   try {        
			bat "cd SQLSource \n ExecScripts.bat"
		
			bat "cd SQLSource \n ExecScripts.bat"
			def logX = readFile "${env.WORKSPACE}/SQLSource/errorM_logfile.txt"
				
			if(logX == '')
					echo " No Error log generated for script M"
			else
					throw err
				
			}
		catch(err){
			echo "Error exists in  Git X Script, Marking build as unstable"
			currentBuild.result = "UNSTABLE"
					   }
        try{
			def logY = readFile "${env.WORKSPACE}/SQLSource/errorO_logfile.txt"
			if (logY == '')
			
				echo "No Error Log generated for Script O"
			else
				throw err}
	   catch(err){
				echo "Error exists in Git Y Script, Marking build as unstable"
				currentBuild.result = "UNSTABLE"
			 }
			
		try{
				def logZ = readFile "${env.WORKSPACE}/SQLSource/errorN_logfile.txt"
				if(logZ == '')
					echo "No Error Log generated for N"
				else 
					throw err}
		catch(err){
				echo "Error exists in Git Y Script, Marking build as unstable"
				currentBuild.result = "UNSTABLE"
			}
        }
       stage ('Tests') {	
	   def status = ""
	     try{
                bat "echo 'shell scripts to run TAF TEST...'"
				bat "java -jar target\\tafd.jar"
				def out= "$JENKINS_HOME/jobs/$JOB_NAME/builds/${BUILD_NUMBER}"
				bat "cd $JENKINS_HOME/jobs/$JOB_NAME/builds/${BUILD_NUMBER} \n dir /b /a-d > tmp.txt"
				def files = readFile "$JENKINS_HOME/jobs/$JOB_NAME/builds/${BUILD_NUMBER}/tmp.txt"
				def temp="tmp.txt";
				bat "java -jar LogParser.jar $out temp.txt"
				status = readFile "$JENKINS_HOME/jobs/$JOB_NAME/builds/${BUILD_NUMBER}/result.txt"
				
				if(status.contains('Unsuccessful')){
						echo status
						throw err 
					}
			}
		catch(err){
				currentBuild.result='UNSTABLE'
		}
            
        }
        stage ('Deploy') {
            //update dashboard
             bat "echo 'will update dashbaord...'"
			 echo "test"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
