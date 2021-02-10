podTemplate(cloud: 'openshift',label: 'builder',
            containers: [
                    containerTemplate(name: 'jnlp', image: 'ninech/jnlp-slave-with-docker', privileged: true, args: '${computer.jnlpmac} ${computer.name}')
                    
            ],
            volumes: [
                    hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
					
            ]) 
{
node{

  def MAVEN_HOME = tool "MY_Maven"
  env.PATH = "${env.PATH}:${MAVEN_HOME}/bin"
  def now = new Date()
  env.TIME = now.format("yyMMdd.HHmm", TimeZone.getTimeZone('UTC'))

stage('Checkout')
{
	
checkout([$class: 'GitSCM', branches: [[name: '*/development']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'snehalgit', url: 'https://github.com/snehaljoshi0904/assetvalidator.git']]])
}
stage('Initial Setup')
{
sh 'mvn clean compile'
}

stage('Unit Testing')
{
sh 'mvn test'
}
stage('Code Coverage')
{
sh 'mvn package'

stash includes: 'Dockerfile', name: 'dfile'
stash includes: 'target/', name: 'efile'
}
stage('SonarQube analysis') 
	{
		withSonarQubeEnv('sonarqube') 
		{
                 sh 'mvn clean package sonar:sonar'
		
    		}
	 }
	
	
stage ("Quality Gate ") 
	/*{
            
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
               
            }
        }*/

	stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
   
}


  
stage('build')
	{
	node('builder'){
				
		container('jnlp') {

			unstash 'dfile'
			unstash 'efile'
			sh 'docker build -t snehalj/assetvalidator:${TIME} .'			
			withCredentials([usernamePassword(credentialsId: 'snehaldockerhub', passwordVariable: 'PWDD', usernameVariable: 'USER')]) {
           			 sh 'docker login -u=$USER -p=$PWDD'
			}
			sh 'docker push snehalj/assetvalidator:${TIME}'
		 }
	}
}


node {
	stage('DV deploy')
	{ 
    sh '/tmp/kubectl create -f orchestration/deployment.yml -n=fields-jenkins-dev'

	}
  }
}
