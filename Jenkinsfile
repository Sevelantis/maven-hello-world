pipeline
{
  agent any
  
  environment
  {
    PRIVATE_KEY = "${env.HOME}/.ssh/tomcat_key"
    JENKINS_WAR_PATH = "${env.WORKSPACE}/target/apigenerator-0.0.1-SNAPSHOT.war"
    TOMCAT_WAR_PATH = 'jenkins_user@tomcat:/usr/local/tomcat/webapps'
  }
  
  stages
  {
    stage("build .war")
    {
      steps
      {
        sh 'pwd'
        sh 'mvn clean package war:war --settings .mvn/wrapper/settings.xml'
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
