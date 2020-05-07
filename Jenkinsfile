//START-OF-SCRIPT
timeout(time:60, unit: 'SECONDS') {
  node ('agent1') {
	properties([
		pipelineTriggers([pollSCM(H/1 * * * 1-5')])
	])
  
    def GRADLE_HOME = tool name: 'gradle-4.10.2', type: 'hudson.plugins.gradle.GradleInstallation'
    sh "${GRADLE_HOME}/bin/gradle tasks"
  
    stage('Clone') {
        git url: 'https://github.com/plimpix/devops-webapp.git'
    }
    
    stage('build') {
        sh "${GRADLE_HOME}/bin/gradle build"
    }
    
    stage('Archive') {
        archiveArtifacts 'build/libs/*.war'
    }
   }
}
//END-OF-SCRIPT
