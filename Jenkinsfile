pipeline {
    agent any
    
    stages {
        stage('Fetch Code') {
            steps {
                
                echo 'Fetching code from GitLab...'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Install any dependencies required for the pipeline
                // For simplicity, assuming dependencies are already installed
                echo 'Installing dependencies...'
            }
        }
        
        stage('Deploy Web Server') {
            steps {
                // Execute the Ansible playbook to deploy Apache HTTP Server
                sh 'ansible-playbook -i inventory/hosts WebServerSetup.yml'
            }
        }
        
        stage('Email Notification') {
            steps {
                script {
                    // Send email notification only if the previous stage failed
                    if (currentBuild.result == 'FAILURE') {
                        emailext subject: "Pipeline failed for ${env.JOB_NAME}",
                                  body: "The pipeline failed for the following reason: ${currentBuild.rawBuild.result}",
                                  to: 'shoroukeid@gmail.com'
                                  replyTo: 'ahmed@gmail.com' 
                    }
                }
            }
        }
    }
    
    post {
        always {
            
            deleteDir()
        }
    }
}
