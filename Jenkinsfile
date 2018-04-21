pipeline {
  agent {
    node {
      label 'Start'
    }

  }
  stages {
    stage('') {
      steps {
        sh '''sh \'virtualenv env -p python3.5\'
sh \'. env/bin/activate\'
sh \'env/bin/pip install -r requirements.txt\''''
      }
    }
  }
}