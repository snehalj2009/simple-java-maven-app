node {
  
  stage("checkout") {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/snehalj2009/simple-java-maven-app.git']]])
  }
  
}
