def dockerImage;

node ('docker'){
  stage('SCM'){
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false,
     extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/ahholden/jenkinstest.git']]])
  }
  stage('Build'){
    dockerImage = docker.build('ahholden/agent-dnc:v$BUILD_NUMBER', './dotnetcore');
  }
  stage('Push'){
    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials'){
      dockerImage.push();
    }
  }
}
