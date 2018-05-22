
/*
podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:1.11', ttyEnabled: true, command: 'cat')],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "jenkins/jnlp-slave"
  node('docker') {
    stage('Docker outside of Docker check') {
      container('docker') {
        sh "docker version"
      }
    }
  }
}
*/


pipeline {
  agent {
    kubernetes {
      label 'declarative-docker'
      podTemplate {
        containerTemplate {
          name 'docker'
          image 'docker:1.11'
          ttyEnabled true
          command 'cat'
        }
        volumes {
          hostPathVolume {
            mountPath '/var/run/docker.sock'
            hostPath '/var/run/docker.sock'
          }
        }
      }
    }
  }
  stages {
    stage('Docker outside of Docker check') {
      steps {
        container('docker-build')
        sh 'docker version'
      }
    }
  }
}
