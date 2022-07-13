/*node{
    def MHD = tool name: "maven3.8.4"
    stage('code'){
        git branch: 'development', url: 'https://github.com/team16flight/web-app.git'
    }
    stage('BUILD'){
       sh "${MHD}/bin/mvn clean package"
 
    }
    /*
    stage('deploy'){
  sshagent(['tomcat']) {
  sh "scp -o StrictHostKeyChecking=no target/*war ec2-user@172.31.15.31:/opt/tomcat9/webapps/"
}
}
stage('email'){
emailext body: '''Build is over

Acada
437212483''', recipientProviders: [developers(), requestor()], subject: 'Build', to: 'tdapp@gmail.com'
}
    */


pipeline{ 
    agent any 
    tools { 
        maven "maven3.8.4" 
    } 
    stages{ 
       stage('1. Git Clone'){ 
           steps{ 
               git "https://github.com/Ufuotech/web-app.git" 
           } 
       }  
       stage('2. Build Package'){ 
           steps{ 
               sh "mvn package" 
           } 
       }
       stage('3. Code Quality'){ 
           steps{ 
               sh "mvn sonar:sonar" 
           } 
       }
    stage('5. Approval'){
                steps{
                    sh "echo Approval for BOA"
                    timeout(time:5, unit:'DAYS'){
                        input message:'Approval for Production'
                    }
                }
             }
              stage('6.predeployment'){
        steps{
            sh "docker build -t ufuodock/cohort7 ."
            sh "docker run --name cohort7 -d -p 2500:8080 ufuodock/cohort7"
        }
     }
    }
}    
