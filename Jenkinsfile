pipeline {
  agent any

  environment{
    DOCKER_IMAGE = 'node-hello-world'
  }

  stages {
    stage('Build') {
      steps {
        script{
            docker.build(DOCKER_IMAGE)
        }
      }
    }
    stage('Test') {
      steps {
        script{
            docker.image(DOCKER_IMAGE).inside{
                sh 'npm install'
                sh 'npm install mocha'
                sh 'npm test'
            }
        }
      }
    }
    stage('Deploy') {
      steps {
            script{
                docker.image(DOCKER_FILE).run('-d -p 3000:3000')
            }
        }
      }
    }
  }