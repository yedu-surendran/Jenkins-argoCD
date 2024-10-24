pipeline {
    agent any

    stages {


        stage('Setup') {
            steps {

                sh "pip install -r requirements.txt"
            
            }
        }
        stage('Test') {
            steps {
                sh "pytest"
                
            }
        }    
        stage('Deployment') {
            input {
                message "Do you want to proceed further?"
                ok "Yes"
            }
            steps {
                echo "Running Deployment"
                
            }
        } 
        
            
    }
}
