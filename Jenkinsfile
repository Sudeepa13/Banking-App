pipeline{
  agent any
  tools{
   maven 'MAVEN_HOME'
  }
   
  environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY') 
  } 
  
  stages{
    stage('checkout git'){
      steps{
          git branch: 'main', url: 'https://github.com/shashikrpet/banking-project.git'
      }
    }
/*
    stage ('maveen package')
    {
      steps{
      sh 'mvn clean package'
        }
    }

    stage ('HTML report')
    {
      steps{
publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/banking-project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      }
    }

    stage('docker file and image')
          {
            steps{
                 sh 'docker build -t shashikrpet/banking-app:1.0 .'
            }
          }
    
stage('Docker image push') {
    steps {
    withCredentials([usernamePassword(credentialsId: 'dockerlog', passwordVariable: 'docker_pwd', usernameVariable: 'docker_usr')]) {
          sh ' docker login -u ${docker_usr} -p ${docker_pwd}'
        }
      sh 'docker push shashikrpet/banking-app:1.0'
      
            }
        }
*/
    stage ('Configure Test-server with Terraform, Ansible and then Deploying'){
            steps {
                dir('my-serverfiles'){
                sh 'sudo chmod 600 Awskeypair.pem'
                sh 'terraform init'
                sh 'terraform validate'
                sh 'terraform apply --auto-approve'
                }
            }
        }


    

/*        stage('Deploy on server'){
          steps{
        ansiblePlaybook credentialsId: 'ubuntu-ssh', disableHostKeyChecking: true, installation: 'ansible', playbook: 'deploy.yml'
          }    
       }
    */
  
    }
}


    
