pipeline
{
  agent any
  
  environment
  {
    SSH_PRIVATE_KEY = "${env.HOME}/.ssh/tomcat_key"
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
    
    stage("ssh authentication tomcat")
    {
      steps
      {
        sh 'pwd'
        sh '. /var/jenkins_home/ssh_auth.sh'
      }
    }
    stage("send && deploy .war")
    {
      steps
      {
        sh 'scp -i ${SSH_PRIVATE_KEY} ${JENKINS_WAR_PATH} ${TOMCAT_WAR_PATH}'
      } 
    }    
  }
  
}
