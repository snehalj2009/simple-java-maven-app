node {
 
 def MAVEN_HOME = tool "MY_Maven"
  env.PATH = "${env.PATH}:${MAVEN_HOME}/bin"
 
stage('checkout') {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/snehaljoshi0904/simple-java-maven-app.git']]])
}

stage('unit testing') {
 sh 'mvn test' 
}

stage('code analysis') {
 echo 'analysis' 
}
}
