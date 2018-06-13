
/*
podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:1.11', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "jenkins/jnlp-slave"
  node('docker') {
    stage('Docker outside of Docker check') {
      container('docker') {
        sh "docker version; docker ps"
      }
    }
  }
}
*/

pipeline {
  agent {
    docker { 
      image 'docker'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
  }
  stages {
    stage('Docker outside of Docker check') {
      steps {
        sh 'docker version'
      }
    }
  }
}

