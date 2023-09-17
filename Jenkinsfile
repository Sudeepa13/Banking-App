pipeline{
  agent any
  tools{
   maven 'MAVEN_HOME'
  }
  
  stages{
    stage('checkout git'){
      steps{
          git branch: 'main', url: 'https://github.com/shashikrpet/Insurance.git'
      }
    }

    stage ('maveen package')
    {
      steps{
      sh 'mvn clean package'
        }
    }

    stage ('HTML report')
    {
      steps{
publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insurance/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      }
    }

    stage('docker file and image')
          {
            steps{
                 sh 'docker build -t shashikrpet/insure-app:2.0 .'
            }
          }
    
stage('Docker image push') {
    steps {
    withCredentials([usernamePassword(credentialsId: 'dockerlog', passwordVariable: 'docker_pwd', usernameVariable: 'docker_usr')]) {
          sh ' docker login -u ${docker_usr} -p ${docker_pwd}'
        }
      sh 'docker push shashikrpet/insure-app:2.0'
      
            }
        }

        stage('Deploy on server'){
          steps{
        ansiblePlaybook credentialsId: 'ubuntu-ssh', disableHostKeyChecking: true, installation: 'ansible', playbook: 'deploy.yml'
          }
        
          
        }
    
  
    }
}


    
