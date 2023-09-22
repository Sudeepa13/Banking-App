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
          git branch: 'main', url: 'https://github.com/Sudeepa13/Banking-App.git'
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
publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/banking-project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      }
    }

    stage('docker file and image')
          {
            steps{
                 sh 'docker build -t sudeedockeracc/banking-app:1.0 .'
            }
          }
    
stage('Docker image push') {
    steps {
  withCredentials([usernamePassword(credentialsId: 'docid', passwordVariable: 'dockerpwd', usernameVariable: 'dockerusr')]) {
          sh ' docker login -u ${dockerusr} -p ${dockerpwd}'
        }
      sh 'docker push sudeedockeracc/banking-app:1.0'
      
            }
        }

   */ stage ('Configure Test-server with Terraform, Ansible and then Deploying'){
            steps {
                dir('my-serverfiles'){
                sh 'sudo chmod 600 Awskeypair.pem'
                sh 'sudo apt-get install terraform'
                sh 'terraform init'
                sh 'terraform validate'
                sh 'terraform apply --auto-approve'
                }
            }
        } */

     
    }
}


    
