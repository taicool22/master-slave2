pipeline{
  agent {
    label {
      label 'slave1'
    }
  }
  stages{
    stage('version-control'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/jenkins-parallel-job.git']]])
      }
    }
    stage('parallel-job'){
      parallel{
        stage('sub-job1'){
          steps{
            echo 'action1'
          }
        }
        stage('sub-job2'){
            agent{
                label'slave2'
            }
          steps{
            echo 'action2'
          }
        }
        stage('sub-job3'){
            steps{
                sh 'whoami'
            }
        }
      }
    }
    stage('codebuild'){
      agent {
        label {
          label 'slave3'
        }
      }
      steps{
        sh 'cat /etc/passwd'
      }
    }
  }
}