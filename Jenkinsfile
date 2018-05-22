
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
      yaml """
apiVersion: v1
kind: Pod
metadata:
  name: buildPod
  labels:
    app: buildPod
spec:
  containers:
  - name: docker-build
    image: docker:1.11
    tty: true
    command:
    - cat
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker-socket
  volumes:
  - name: docker-socket
    hostPath:
      path: /var/run/docker.sock
      type: File
"""
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
