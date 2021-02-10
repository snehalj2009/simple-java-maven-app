node{
stage('clone') {
  
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/snehaljoshi0904/simple-java-maven-app.git']]])
}
}
