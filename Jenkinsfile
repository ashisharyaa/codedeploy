currentBuild.displayName = "MyWebBuild-#"+currentBuild.number
pipeline{
  agent any
  stages{
      stage("Git Checkout"){
          steps{
          
          
              git credentialsId: 'MyGitHub', url: 'https://github.com/ashisharyaa/mahalogin.git'
          
            }
            
            }
            
            stage("Maven Build"){
              steps{
                
                sh "mvn clean package"
                sh "mv target/*.war target/mahaLogin.war"
                
                
                
            }
            
            }
            
            stage("Deploy jenkins to tomcat"){
                steps{
                
                sshagent(['root']) {
                
                 sh """
                    scp -o StrictHostKeyChecking=no target/mahaLogin.war ec2-user@172.31.88.163:/opt/tomcat9/webapps/
                    
                    ssh  root@172.31.88.163 /opt/tomcat9/bin/shutdown.sh
                    
                    ssh  root@172.31.88.163 /opt/tomcat9/bin/startup.sh
                    
                    """
                    
                    }
       
              
              }
  
  
        }
  
    }
}
