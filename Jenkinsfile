pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}!"
        sh 'java -version'
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
      }
    }
          stage('Testing') {
        parallel {
          stage('Java 7') {
            agent { label 'jdk7' }
            steps {
              container('maven') {
                sh 'mvn -v'
              }
            }
          }
          stage('Java 8') {
            agent { label 'jdk8' }
            steps {
              container('maven') {
                sh 'mvn -v'
              }
            }
          }
        }
      }
  }
  environment {
    MY_NAME = 'Mary'
    TEST_USER = credentials('test-user')
  }
  post {
    aborted {
      echo 'Why didn\'t you push my button?'
      
    }
    
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
}
