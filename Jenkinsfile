node('docker') {
  stage('SCM') {
    checkout poll: false, scm: [$class: 'GitSCM', branches: [[name: '/develop']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/freitasvazthiago/docker_workspace']]]
  }
  stage('SonarQube Analysis') {
        sh "/home/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonarqubescanner/bin/sonar-scanner -Dsonar.host.url=http://172.21.0.45:9000 -Dsonar.projectName=meanstackapp -Dsonar.projectVersion=1.0 -Dsonar.projectKey=meanstack:app -Dsonar.sources=. -Dsonar.projectBaseDir=/home/jenkins/workspace/sonarqube_test_pipeline"
    }
  }
