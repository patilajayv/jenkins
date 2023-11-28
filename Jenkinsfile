pipeline {
    agent any
    
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/patilajayv/Jenkins.git'            }
        }
        
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'  // Install dependencies using pip
            }
        }
        
        stage('Test') {
            steps {
                sh 'pytest'  // Run unit tests using pytest
            }
        }
        
        stage('Deploy') {
            steps {
                // Add deployment steps to staging environment if tests pass
                // sh 'python3 app.py'  // Example deployment script
                sh 'pip install gunicorn'
                sh 'nohup gunicorn -w 4 -b 0.0.0.0:8000 app:app > gunicorn.log 2>&1 &'
            }
        }
    }
    
    post {
        success {
            mail bcc: '', body: 'hello build is successful', cc: '', from: '', replyTo: '', subject: 'email form jenkins', to: 'patilajayv2201@gmail.com'
            // mail to: 'lokesh.sayana@email.com', 
            //      subject: 'Build Success', 
            //      body: 'Your Jenkins build succeeded!'
        }
        failure {
            mail bcc: '', body: 'hello build is unsuccessful', cc: '', from: '', replyTo: '', subject: 'email form jenkins[[failure!!!!!!!!]]', to: 'patilajayv2201@gmail.com'
            // mail to: 'lokesh.sayana@email.com', 
            //      subject: 'Build Failure', 
            //      body: 'Your Jenkins build failed!'
        }
    }
}
