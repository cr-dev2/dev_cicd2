pipeline 
{ 
agent any 
stages 
{

stage('Checkout')
 {
 steps 
 { 
 
 checkout([$class: 'GitSCM', branches: [[name: '*/CICD_Test']],
     userRemoteConfigs: [[credentialsId: '9d379816-40aa-43ff-9f6c-8015f4936219'],[url: 'https://github.com/whitbread-costa-retail/cm-x-sendgrid-api.git']]])
 echo 'Hello World' 
 } 
 } 
 }
} 
 
 