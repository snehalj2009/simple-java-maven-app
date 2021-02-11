node {
stage('checkout') {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/snehaljoshi0904/simple-java-maven-app.git']]])
}

stage('unit testing') {
 echo 'unit testing' 
}

stage('code analysis') {
 echo 'analysis' 
}
}
