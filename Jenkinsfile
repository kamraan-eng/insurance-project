pipeline{
    
    agent any
    
    tools{
        maven 'mymaven'
    }
    
    stages{
        stage('Clone Repo')
        {
            steps{
                git 'https://github.com/kamraan-eng/banking-finance-Project1.git'
            }
        }
        stage('Test Code')
        {
            steps{
                sh 'mvn test'
            }
        }
        
        stage('Build Code')
        {
            steps{
                sh 'mvn package'
            }
        }
        stage('Build Image')
        {
            steps{
                sh 'docker build -t myproject1:$BUILD_NUMBER .'
            }
        }
        
        stage('Deploy the Image')
        {
            steps{
                sh 'docker run -d -P myproject1:$BUILD_NUMBER '
            }
        }
         stage('push to dockerhub')
        {
            steps{
                sh 'docker login -u kamraan1 -p Kamraan@123'
                sh 'docker tag myproject1:$BUILD_NUMBER kamraan1/myproject1:$BUILD_NUMBER'
                sh 'docker push kamraan1/myproject1:$BUILD_NUMBER'
            }
        }         
        }
        
    stage('Configure and Deploy to the test-server'){
        ansiblePlaybook become: true, credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml'
    }
        
        
    }
}




