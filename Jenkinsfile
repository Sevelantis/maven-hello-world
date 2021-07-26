pipeline
{
  agent any
  
  environment
  {
    PRIVATE_KEY = "${env.HOME}/.ssh/tomcat_key"
    JENKINS_WAR_PATH = "${env.WORKSPACE}/target/*.war"
    TOMCAT_WAR_PATH = 'jenkins_user@tomcat:/usr/local/tomcat/webapps'
  }
  
  stages
  {
    stage("build .war")
    {
      steps
      {
        sh 'pwd'
        sh 'mvn clean package war:war'
      } 
    }
    
    stage("ssh-auth-tomcat")
    {
      steps
      {
        sh '. /var/jenkins_home/ssh_auth.sh'
      }
    }
    stage("send .war")
    {
      steps
      {
        
        sh 'scp -i ${PRIVATE_KEY} ${JENKINS_WAR_PATH} ${TOMCAT_WAR_PATH}'
        
      } 
    }
    
    stage("deploy")
    {
      steps
      {
        echo 'deploying the appplication'
      } 
    }
    
  }
}
