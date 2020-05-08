pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Security Scan') {
              steps { 
                  aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: '', onDisallowed: 'ignore', outputFormat: 'html'
              }
         }         
        stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'aws-user-waqas-secret-key') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'my-aws-bucket-120')
                  }
              }
         }
     }
}
