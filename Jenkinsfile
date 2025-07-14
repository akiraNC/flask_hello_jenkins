pipeline {
  agent {
    kubernetes {
      label 'jenkins-agent-my-app'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: ci
spec:
  containers:
  - name: jnlp
    image: jenkins/inbound-agent:latest
    args: ['\$(JENKINS_SECRET)', '\$(JENKINS_NAME)']
  - name: python
    image: python:3.7
    command:
    - cat
    tty: true
"""
    }
  }
  stages {
    stage('Test python') {
      steps {
        container('python') {
          sh 'pip install -r requirements.txt'
          sh 'python test.py'
        }
      }
    }
  }
}
